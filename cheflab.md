## Chef Lab:

#### **This part of Lab describes how to setup the Chef workstation and start creating workbooks and recipes**

##### Workstation:
### Create workstation
####  download  chef-workstation
From the **chef downloads** site https://downloads.chef.io/products/workstation, select the OS and download the required version,
once download started, browser tab pause download and rightclik on the url, copy the link and run below command
```
#wget https://packages.chef.io/files/stable/chef-workstation/20.10.168/ubuntu/20.04/chef-workstation_20.10.168-1_amd64.deb
```
This will download the package to the workstation node
##### for ubuntu run below command to install chef, 
**#dpkg -i chef-workstation_20.10.168-1_amd64.deb**
###### Once the chef is installed, verify the version with below command, to ensuer it is installed
#### #chef --version

**Create cookbooks directory later we create  all the cookbook**
#### #mkdir cookbooks

#### under cookbooks directory create cookbooks
## chef genrerate cookbook <cookbook-name>
#### #chef genrerate cookbook new-cookbook
After creating the chef cookbook, in the cookbook directory,  default files are created like, <br>
1. chefignore  <br>
2. kitchen.yml for testing the cookbook <br>
3. metadata.rb     --> name,version,author of the cookbook <br>
4. readme          --> information about the cookbook, user group etc <br>
5. recipie         --> is the code file <br>
6. spec            --> for unit testing <br>
7. test            --> for integration test  <br>

### create recipie
#### chef generate recipie <recipie-name> <br>
### #chef generate recipe new-recipe <br>
which creates recipie file in default recipes directory <br>
##### Add the content into the recipe file  as show below <br>

### new-recipie.rb file is like below, which consists of code: <br>
file '/newfile' do             --> File name to be created and "do" means create <br>
content 'Chef new file'        --> Content in the file, after creation of the file, chef will place the content <br>
action :create                 --> Create the file <br>
end                            --> end of the task <br>

### To ensure no syntax error of the file 
```
#### #chef exec ruby -c new-cookbook/recipes/new-recipie.rb 

```
#### Run the chef-client to execute the recipe

```json
 #chef-client -zr "recipe[new-cookbook::new-recipie]"
```
#### On successful run it produces the output as 


Starting Chef Infra Client, version 16.6.14
Patents: https://www.chef.io/patents
resolving cookbooks for run list: ["new-cookbook::new-recipe01"]
Synchronizing Cookbooks:
  - new-cookbook (0.1.0)
Installing Cookbook Gems:
Compiling Cookbooks...
Converging 1 resources
Recipe: new-cookbook::new-recipe01
  * file[/newfile] action create
    - create new file /newfile
    - update content in file /newfile from none to d3b7c9
    --- /newfile   2020-10-28 19:45:59.780289866 +0000
    +++ /.chef-falafal20201028-8246-ckf0aa 2020-10-28 19:45:59.780289866 +0000
    @@ -1 +1,2 @@
    +Chef new file
Running handlers:
Running handlers complete
Chef Infra Client finished, 1/1 resources updated in 01 seconds

#### Creating multiple recipes
####	Using knife transfet the code to server

### to execute this file, run as below
### chef-client -zr "recipie[new-cookbook::new-recipie02]"  --> this creates a new file as "newfile"

---

```
package 'tree' do   --> package installation <br>
action :install    --> spefifying the action <br>
end <br>

file 'testfile' do   --> speify the file <br>
content 'Chef test file' --> content of the file <br>
action :create            --> action on the files <br>
owner 'root'              --> owner and group of the file  <br>
group 'root'
end <br>


package 'httpd' do   --> install httpd package <br>
action :install <br>
end <br>

file '/var/www/html/index.html' do  --> content in index.html  <br>
content 'First delecious recipe' <br>
action :create   --> create the file <br>
end <br>


service 'httpd' do             --> start the httpd service <br>
action [:enable, :start]  <br>
end  <br>
```
