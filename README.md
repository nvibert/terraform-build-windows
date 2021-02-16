# terraform-build-windows
A sample script to build a provider in Windows and move it to the right folder
When you want to compile a Terraform provider, it's sometimes confusing to work out how to do it and in which folder to push it.
It's even more confusing in Windows when you spend most of your time on a Mac.


## Assumptions and Format

The format used in the create-terrraform-provider-windows.txt assumes your provider is leveraging the following syntax.
Obviously, replace "vmware.com", "edu" and "ctoa" as per your preference.

For more details, check out the details on the HashiCorp [website](https://www.terraform.io/docs/language/providers/requirements.html).

```hcl
terraform {
  required_providers {
    ctoa = {
      source  = "vmware.com/edu/ctoa"
    }
  }
}
```

## Requirements:

- Git.
- Terraform.
- Go. 

## Usage:

From the command terminal:

Clone the following [repo](https://github.com/adeleporte/ctoa-hacknite.git) with the following command:  
`git clone https://github.com/adeleporte/ctoa-hacknite.git`

Navigate to the Terraform folder:  

`cd ctoa-hacknite\terraform-provider-ctoa`

Create a folder where the compiled provider will be moved to.  
`mkdir -p %APPDATA%\terraform.d\plugins\vmware.com\edu\ctoa\0.1\windows_amd64`

Compile the provider:  

`go build -o terraform-provider-ctoa.exe`

Move the provider to the correct location:  

`move terraform-provider-ctoa.exe %APPDATA%\terraform.d\plugins\vmware.com\edu\ctoa\0.1\windows_amd64`

Assuming you're still in `terraform-provider-ctoa` and in the same folder as the `main.tf` file, the initialization should work:  
`terraform init`
