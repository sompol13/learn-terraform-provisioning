## Provision Infrastructure with Cloud-Init
Companion code repository for learning to provision Terraform instances with `cloud-init`

### Create a local SSH key
Generate a new SSH key in your terminal called tf-cloud-init

### Add your public SSH key to your cloud-init script
Open the scripts/add-ssh-web-app.yaml file and paste the contents of tf-cloud-init.pub into the user data ssh_authorized_keys section.

### Add the cloud-init script to the Terraform configuration
Open the main.tf file. Notice how the template_file.user_data data block retrieves the contents of the add-ssh-web-app.yaml file. Then, it is passed into aws_instance.web as a user_data value to be initialized when the instance is created.
-`terraform init`
-`terraform apply`

### Verify your instance
Connect to your instance via SSH by piping the aws_instance.web.public_ip resource attribute to the terraform console command.
-`ssh terraform@$(terraform output -raw public_ip) -i ../tf-cloud-init`

*Navigate to the Go directory.*
-`cd go/src/github.com/hashicorp/learn-go-webapp-demo`

*Launch the demo webapp.*
-`go run webapp.go`

<img width="1608" alt="2" src="https://user-images.githubusercontent.com/33342822/150629317-81774f13-c1b4-4f3b-b6f2-271911c8da28.png">
