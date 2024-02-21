# *移機備份
## 1.帳號設定資料庫備份
<code>cd harbor
docker-compose down
cp harbor.yml /my_backup_dir/
cp -r /data/database /my_backup_dir/
</code>

## 2.容器Image、Helm charts備份
<code>cp -r /data/registry /my_backup_dir/
cp -r /data/chart_storage /my_backup_dir/
</code>

## 3.其他資料備份
<code>cp -r /data/trivy-adapter /my_backup_dir/
</code>
</p>

# *Harbor安裝
### pre-require:
* docker
* docker-compose

### Check config setting
* harbor.yml

### Install Harbor
<code>wget https://github.com/goharbor/harbor/releases/download/v2.1.1/harbor-online-installer-v2.1.1.tgz
tar -xvf harbor-online-installer-v2.1.1.tgz
mkdir /data
cp -r /my_backup_dir/. /data/
rm /data/harbor.yml
cd harbor/
cp -f /my_backup_dir/harbor.yml .
sudo ./install.sh --with-chartmuseum --with-trivy
docker-compose top
</code>
