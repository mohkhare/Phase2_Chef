node('master') {
    checkout scm

    def node_name           = 'chefAutoMat248'
    def vm_ip               = '10.118.41.248/24'
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
                bat(/knife cookbook list/)
            }

        }    

        stage('Check Knife vsphere'){
                        
            if (isUnix()) {
                sh "knife vsphere template list"
            } else {
                bat(/knife vsphere template list/)
            }

        }      

                
        stage('Creat VM') {

            if (isUnix()) {
                sh "knife vsphere vm clone ${node_name} --template ${vm_template} --start true --node-name ${node_name} --resource-pool ${vm_resource_pool} --cspec ${vm_spec} --cips ${vm_ip} --cdomain ${vm_domain} --verbose"
            } else {
                bat(/knife vsphere vm clone "${node_name}" --template "${vm_template}" --start true --node-name "${node_name}" --resource-pool "${vm_resource_pool}" --cspec "${vm_spec}" --cips "${vm_ip}" --cdomain "${vm_domain}" --verbose/)
            }
        }
        
        
        // stage('Add VM as chef node') {

        //     if (isUnix()) {
        //         sh "knife bootstrap 10.118.41.247 --ssh-user root --ssh-password Password1 --node-name chefAutoMat247 --sudo --verbose"
        //     } else {
        //         bat(/knife bootstrap 10.118.41.247 --ssh-user root --ssh-password Password1 --node-name chefAutoMat247 --sudo --verbose/)
        //     }
        // }

        // stage('Install docker on VM') {

        //     stage('Add recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list add chefAutoMat241 'role[dockerinstall]'"
        //         } else {
        //             bat(/knife node run_list add chefAutoMat241 'role[dockerinstall]'/)
        //         }
        //     }
        //     stage('run recipe on node') {
    
        //         if (isUnix()) {
        //             sh "knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose"
        //         } else {
        //             bat(/knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose/)
        //         }
        //     }
        //     stage('Remove recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list remove chefAutoMat241 'role[dockerinstall]'"
        //         } else {
        //             bat(/knife node run_list remove chefAutoMat241 'role[dockerinstall]'/)
        //         }
        //     }
        // }
        // stage('Pull and run container') {

        //     stage('Add recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list add chefAutoMat241 'role[dockerrun]'"
        //         } else {
        //             bat(/knife node run_list add chefAutoMat241 'role[dockerrun]'/)
        //         }
        //     }
        //     stage('run recipe on node') {
    
        //         if (isUnix()) {
        //             sh "knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose"
        //         } else {
        //             bat(/knife ssh 'name:chefAutoMat241' 'sudo chef-client' -a ipaddress --ssh-user root --ssh-password Password1 --verbose/)
        //         }
        //     }
        //     stage('Remove recipe') {
    
        //         if (isUnix()) {
        //             sh "knife node run_list remove chefAutoMat241 'role[dockerrun]'"
        //         } else {
        //             bat(/knife node run_list remove chefAutoMat241 'role[dockerrun]'/)
        //         }
        //     }
        // }

    }
}

