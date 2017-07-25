node('master') {
    checkout scm

    // modify node_name and ip address fields  //
    // ---------------------------------------//
    def node_name           = 'chefAutoMat241'
    def vm_ip               = '10.118.41.241'
    //---------------------------------------//

    def vm_template         = 'CentOsTemplate'
    def vm_resource_pool    = 'Compute/Chef_Test'
    def vm_spec             =  'CentOs_Chef'
    def vm_domain           =  'csa.local'
    def ssh_user            = 'root'
    def ssh_pwd             = 'Password1'


    dir('chef-repo'){

        stage('Get Chef Repo'){
                        
            git 'https://github.com/devopsevd/chef_docker_cookbooks.git'

        }
        
        stage('Check Knife cookbook'){
                        
            if (isUnix()) {
                sh "knife cookbook list"
            } else {
                //bat(/knife cookbook list/)
            }

        }    

        // stage('Check Knife vsphere'){
                        
        //     if (isUnix()) {
        //         sh "knife vsphere template list"
        //     } else {
        //         //bat(/knife vsphere template list/)
        //     }

        // }      


                
        stage('Creat VM') {

            if (isUnix()) {
                sh "knife vsphere vm clone ${node_name} --template ${vm_template} --start true --node-name ${node_name} --resource-pool ${vm_resource_pool} --cspec ${vm_spec} --cips '${vm_ip}/24' --cdomain ${vm_domain} --verbose"
            } else {
                //bat(/knife vsphere vm clone "${node_name}" --template "${vm_template}" --start true --node-name "${node_name}" --resource-pool "${vm_resource_pool}" --cspec "${vm_spec}" --cips "${vm_ip}" --cdomain "${vm_domain}" --verbose/)
            }
        }
        
        
        stage('Add VM as chef node') {
            // timeout(time: 30, unit: 'SECONDS'){
            //     waitUntil{
            //         //def ret = sh(script: "ping ${vm_ip}", returnStatus: true)
            //         //println ret
            //         return false
            //     }
            // }

            sleep 45

            if (isUnix()) {
                sh "knife bootstrap ${vm_ip} --ssh-user ${ssh_user} --ssh-password ${ssh_pwd} --node-name ${node_name} --sudo --verbose"
            } else {
                //bat(/knife bootstrap 10.118.41.247 --ssh-user root --ssh-password Password1 --node-name chefAutoMat247 --sudo --verbose/)
            }
        }

        stage('Install docker on VM') {

            stage('Add recipe') {
    
                if (isUnix()) {
                    sh "knife node run_list add ${node_name} 'role[dockerinstall]'"
                } else {
                    //bat(/knife node run_list add chefAutoMat241 'role[dockerinstall]'/)
                }
            }
            stage('run recipe on node') {
    
                if (isUnix()) {
                    sh "knife ssh 'name:${node_name}' 'sudo chef-client' -a ipaddress --ssh-user ${ssh_user} --ssh-password ${ssh_pwd} --verbose"
                } else {
                    //bat(/knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose/)
                }
            }
            stage('Remove recipe') {
    
                if (isUnix()) {
                    sh "knife node run_list remove ${node_name} 'role[dockerinstall]'"
                } else {
                   // bat(/knife node run_list remove chefAutoMat241 'role[dockerinstall]'/)
                }
            }
        }
        stage('Pull and run container') {

            stage('Add recipe') {
    
                if (isUnix()) {
                    sh "knife node run_list add ${node_name} 'role[dockerrun]'"
                } else {
                    //bat(/knife node run_list add chefAutoMat241 'role[dockerrun]'/)
                }
            }
            stage('run recipe on node') {
    
                if (isUnix()) {
                    sh "knife ssh 'name:${node_name}' 'sudo chef-client' -a ipaddress --ssh-user ${ssh_user} --ssh-password ${ssh_pwd} --verbose"
                } else {
                    //bat(/knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose/)
                }
            }
            stage('Remove recipe') {
    
                if (isUnix()) {
                    sh "knife node run_list remove ${node_name} 'role[dockerrun]'"
                } else {
                    //bat(/knife node run_list remove chefAutoMat241 'role[dockerrun]'/)
                }
            }
        }

    }
}

