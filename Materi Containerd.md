# Containerd: Pengenalan dan Fungsionalitas

## Apa itu Containerd?
Containerd adalah runtime container open-source yang digunakan untuk mengelola siklus hidup container di lingkungan cloud-native. Containerd bertanggung jawab untuk mengunduh, mengeksekusi, dan mengelola container images, serta menyediakan interface untuk operasi seperti snapshotting, container lifecycle management, dan resource monitoring.

## Fitur Utama Containerd
1. **Runtime yang Ringan**: Containerd memiliki footprint yang kecil namun memiliki kemampuan manajemen yang lengkap.
2. **Modularitas**: Mendukung berbagai plugin dan dapat diperluas dengan mudah.
3. **Integrasi dengan CRI**: Containerd digunakan sebagai runtime utama untuk Kubernetes melalui Container Runtime Interface (CRI).
4. **Snapshotter**: Mendukung snapshot berbasis overlay, Btrfs, dan lainnya untuk pengelolaan layer image.
5. **Gambar dan Distribusi**: Mendukung OCI Image Format dan distribusi image dengan berbagai registries.

## Arsitektur Containerd
Containerd terdiri dari beberapa komponen utama:
- **Client**: Interface yang digunakan untuk berinteraksi dengan containerd melalui API.
- **Containerd Daemon**: Proses utama yang mengelola container.
- **Shims**: Komponen perantara antara daemon dan container runtime seperti runc.
- **Snapshotter**: Mengelola filesystem untuk container images.
- **Content Store**: Menyimpan blob seperti layer image dan metadata.

## Manfaat Menggunakan Containerd
Kinerja yang Tinggi: Karena desainnya yang minimalis, Containerd menawarkan kinerja yang lebih baik dibandingkan runtime lain.
Reliabilitas: Digunakan secara luas di industri, memastikan stabilitas dan dukungan yang baik.
Komunitas dan Dukungan: Memiliki komunitas yang aktif serta dukungan dari CNCF, menjamin pengembangan yang berkelanjutan.

## Instalasi Containerd
Berikut adalah langkah-langkah instalasi Containerd pada distribusi Linux berbasis Debian:

```bash
# Update daftar paket
sudo apt-get update

# Install dependensi
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

# Tambahkan GPG key untuk Containerd
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Tambahkan Docker repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Install Containerd
sudo apt-get update
sudo apt-get install -y containerd.io

# Mulai dan aktifkan layanan Containerd
sudo systemctl start containerd
sudo systemctl enable containerd

## Instalasi Containerd

# Tarik image dari registry
sudo ctr image pull docker.io/library/hello-world:latest

# Jalankan container
sudo ctr run --rm -t docker.io/library/hello-world:latest hello-world

# Contoh konfigurasi kubelet menggunakan Containerd
kind: KubeletConfiguration
apiVersion: kubelet.config.k8s.io/v1beta1
containerRuntime: remote
containerRuntimeEndpoint: unix:///run/containerd/containerd.sock

