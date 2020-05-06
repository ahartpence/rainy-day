In the Google Cloud Console UI, using the project that the disk exists in
* Click on the disk, and create a snapshot. Take note of the name of the snapshot and the region that it's being deployed to
* Click on the newly created snapshot, near the bottom of the screen click on Equivalent Rest
* Take down the `selfLink` address

On the Command Line:
* `gcloud config set project [PROJECT YOU WANT TO CREATE THE DISK IN]`
* `gcloud compute disks create [NAME OF DISK] --source-snapshot=https://www.googleapis.com/compute/v1/[PASTE selfLink HERE] --type=pd-sd --size=[SIZE] --zone [REGION --project=[PROJECT]`
