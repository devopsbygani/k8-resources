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

* d. Create a PersistentVolume (PV)

* e. Create a PersistentVolumeClaim (PVC)

* f. Attach the PVC to a Pod
