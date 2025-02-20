# virtualisation-proxmox
Scripts Bash pour automatiser la création de VMs sous Proxmox.
#!/bin/bash
VM_ID=101
VM_NAME="TestVM"
ISO_PATH="/var/lib/vz/template/iso/ubuntu-22.04.iso"
MEMORY=4096
CORES=2
DISK_SIZE="30G"

echo "Création de la VM..."
qm create $VM_ID --name $VM_NAME --memory $MEMORY --cores $CORES --net0 virtio,bridge=vmbr0
qm importdisk $VM_ID $ISO_PATH local-lvm
qm set $VM_ID --boot c --bootdisk scsi0 --scsihw virtio-scsi-pci --scsi0 local-lvm:$DISK_SIZE
qm start $VM_ID
echo "VM $VM_NAME créée avec succès !"
