# velociraptor-to-timesketch

**We will be working on making this a pre-baked AMI, but here are the deployment steps in the meantime <3**

**Note:** You may need to add/modify `fs.inotify.max_user_watches` in `/etc/sysctl.conf`. The default is 8192, and you may need to increase this number. Run `sysctl -p` after modifying.


### Deployment
* Deploy Timesketch instance - [Deployment Directions](https://github.com/google/timesketch/blob/master/docs/getting-started/install.md)
* python3/pip3 is required, and the awscli
  ```
  apt install python3 python3-pip 
  pip3 install --upgrade awscli
  ```
* Configure AWS CLI
  ```
  aws configure 
  ```
* Modify vars/scripts as necessary with S3 bucket name(s)
* Add Velociraptor artifact in Velociraptor and configure with AWS S3 bucket, region, and IAM credentials
  <img width="924" alt="Screen Shot 2021-07-08 at 2 36 18 PM" src="https://user-images.githubusercontent.com/1244979/124973850-114cdc80-dffa-11eb-8267-fc97488993b2.png">
* Run deploy.sh
  ```
  bash deploy.sh
  ```
* Kick off `Windows.KapeFiles.Targets` collection on one or more clients in Velociraptor
  * Wait for triage zip to upload to S3
  * Wait for zip to download to Timesketch instance from S3
  * log2timeline will begin processing data into a Plaso file
  * timesketch_importer will then bring it into Timesketch
