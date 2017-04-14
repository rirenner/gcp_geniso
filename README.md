# gcp_geniso

exporting an image instructions: https://cloud.google.com/compute/docs/images/export-image

build instance to desired state:
[API call here]

stop instance:
[API call here]

snapshot instance:
[API call here]

create disk from snapshot:
[API call here]

create temp disk larger than original:
gcloud compute disks create temporary-disk --size 15GB --project=[your-projectname]

create temp instance to mount both from:
gcloud compute instances create aciexportimage --scopes storage-rw --disk name=disk-1,device-name=disk-1 --disk name=temporary-disk,device-name=temporary-disk

mount and dd after fs creation also install genisoimage:
[ansible script]

raw disk and geniso:
in this case was vmdk output more likely qcow2 etc..
qemu-img convert -O vmdk disk.raw aciexportimage.vmdk

[ansible script]

cp to cloud storage with gsutil:
    3  gsutil cp aciexportimage.tar.gz gs://[your-bucketname]
    4  gsutil cp aciexportimage.iso gs://[your-bucketname]
    5  gsutil cp aciexportimage.vmdk gs://[your-bucketname]

make bucket public or share between projects etc...
[API call here]
