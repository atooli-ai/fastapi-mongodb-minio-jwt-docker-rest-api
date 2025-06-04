1、安装 s3fs-fuse：
# Ubuntu/Debian
sudo apt-get install s3fs

# CentOS/RHEL
sudo yum install s3fs-fuse

2、创建凭证文件
echo "username:password" > ~/.passwd-s3fs
chmod 600 ~/.passwd-s3fs

3、创建挂载点
sudo mkdir -p /mnt/minio-data
sudo chmod 777 /mnt/minio-data

4、挂载 MinIO 存储：
s3fs minio-bucket /mnt/minio-data \
    -o url=http://localhost:9000 \
    -o use_path_request_style \
    -o passwd_file=${HOME}/.passwd-s3fs

5、开机自启
# 编辑 /etc/fstab
echo "s3fs#minio-bucket /mnt/minio-data fuse _netdev,allow_other,use_path_request_style,url=http://localhost:9000,passwd_file=${HOME}/.passwd-s3fs 0 0" | sudo tee -a /etc/fstab

