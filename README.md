> **Deployment Documentation**

Date : Jun 08, 2023 Author:

-   Phuc NguyenHoang ( [phuc.nguyenhoang@idsolutions.com.vn]{.underline}
    )

-   Khoa Nguyen ( [khoa.nguyen@idsolutions.com.vn]{.underline} )

-   

Here is the documentation to deploy or run with Belga website FO
project. Please note these info to help you deploy easily:

1.  If you work on a new server, please start from \"Step 1: Set up the
    Server\"

2.  If you want to change the URL setting, please start from \"Step 6:
    Build and Bundle and start the Nextjs Project\"

**Note: Please ignore these steps if you installed it on your
environment.**

1.  **Git information:**

Belga Git account:

Account: belga/BelgaIds

Branch: master

2.  **Prerequisites:**

Before proceeding with the deployment, ensure you have the following:

**Step 1**: Set up the Server:

1.  Connect to your server via SSH using a terminal or an SSH client. (
    we use Termius )

2.  Update the system packages by running the following commands:

sudo apt update

sudo apt list \--upgradable

**Step 2**: Install Git

1.  Install Git by running the following command:

sudo apt install git

2.  Verify the installation by checking the Node.js and npm versions:

git \--version

**Step 3**: Install and Configure NVM, Node.js, npm and yarn

1.  Install NVM by running the following command:

> sudo apt-get install wget

wget -qO-
https://raw.githubusercontent.com/creationix/nvm/v0.39.0/install.sh \|
bash source \~/.profile

2.  Verify the installation by checking the nvm versions:

nvm \--version

=\> 0.39.0

3.  Install Node.js with NVM and use node version 16.xx.xx with nvm by
    running the following command:

nvm install 16 nvm use 16

4.  Verify the installation by checking the Node.js and npm versions:

node --version =\> v16.20.0

npm --version

=\> 9.6.7

5.  Install Yarn with node version 16.20.0 by running the following
    command:

npm install -global yarn

6.  Verify the installation by checking the Yarn versions:

yarn -v

=\> 1.22.19

**Step 4**: Install PM2

1.  Install PM2 by running the following command:

> sudo npm i -g pm2

2.  Verify the installation by checking the PM2 versions:

pm2 \--version

=\> 5.3.0

**Step 5**: Clone the Nextjs Project

5.1. Change to the desired directory where you want to clone the
project:

cd /data/ids

5.2.Clone the Nextjs project repository by running the following
command:

git clone
[[http://git.idsolutions.com.vn/belga-ai/belga-website-2023-fo.git]{.underline}](http://git.idsolutions.com.vn/belga-ai/belga-website-2023-fo.git)

**Step 6**: Install Project Dependencies 5.1. 6.1 Change to the project
directory:

cd belga-website-2023-fo/ git checkout phase3

6.2. Install the project dependencies by running the following command:

yarn install

**Step 7**: Build and Bundle and start the Nextjs Project:

You can see '**.env.belga**' files and properties:

NEXT_PUBLIC_API_BASE=http://strapi-belga.staging.belga.be:1337

Please **replace**
["[http://strapi-belga.staging.belga.be:1337]{.underline}"](http://strapi-belga.staging.belga.be:1337/)
by the new link, **for example**:

NEXT_PUBLIC_API_BASE= https://strapi-stg.belga.be

7.1.Build the Nextjs project by running the following command:

yarn build:belga

7.2.Start the Nextjs server by running the following command, we will
use pm2 with version v5.3.0 to deploy (please install pm2 if you haven't
installed yet):

pm2 start yarn \--name \"belga-website-2023-fo\" \-- start

7.3.List all processes with pm2

pm2 list

Note: please find the process id with the name \"belga-website-2023-fo\"
that we have on step 2.

7.4.Check logs of process with pm2 from process id that we found on step
3

pm2 logs \<id the process what you want to check logs\>

7.5.Please monitor the logs file and found the problem.

7.6.If you installed FO with pm2, you should delete it with command:

pm2 delete \<id the process what you want to delete\>
