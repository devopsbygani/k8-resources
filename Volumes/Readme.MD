# Usage of Volumes in Kubernetes

We have two options:

* a. Static Provisioning  
* b. Dynamic Provisioning

# Prerequisites for Static Provisioning

* a. Create an AWS EBS Volume  
  - Have a pre-created EBS volume available  
  - Example Volume ID: `vol-767sdjgdvdjfd`

* b. Install the AWS EBS CSI Driver  
  - Apply the official CSI driver for EBS using the following command:  
    ```bash
    kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.43"
    ```
  - Reference: [AWS EBS CSI Driver GitHub Repository](https://github.com/kubernetes-sigs/aws-ebs-csi-driver.git)

* c. Attach IAM Policy to Node IAM Role  
  - Attach the `AmazonEBSCSIDriverPolicy` to the IAM role associated with your node group

# provisioning

* a. Create a PersistentVolume (PV)

* b. Create a PersistentVolumeClaim (PVC)

* c. Attach the PVC to a Pod

# Prerequisites for Dynamic Provisioning

* a. Install the AWS EBS CSI Driver  
  - Apply the CSI driver using:  
    ```bash
    kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.43"
    ```

* b. Attach IAM Policy to Node IAM Role  
  - Attach the `AmazonEBSCSIDriverPolicy` to the IAM role associated with your node group

* c. Create a StorageClass  
  - Define a `StorageClass` specifying the provisioner and volume type

* d. Create a PersistentVolumeClaim (PVC)  
  - Reference the `StorageClass` in the PVC; Kubernetes will dynamically provision the volume

* e. Attach the PVC to a Pod  
  - Use the PVC in a Pod to mount the dynamically created volume