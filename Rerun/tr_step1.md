# Geçmişin kaydedilmesi ve Github Reposuna Atılması

### history.txt dosyasının oluşturulması.
Aşağıda verilen komutu kullanarak otomatik olarak filtrelenmiş çıktıyla history.txt dosyasını oluşturabilirsiniz.

```
// history | sed 's/^[[:space:]][0-9]+[[:space:]]//' | grep -vE '^(history|myscript.sh)' > history.txt
history | awk '{$1="";print substr($0,2)}' | grep -vE '^(history|myscript.sh)' >> history.txt
```

Oluşan histor.txt dosyasının içinin bu şekil olduğu farz edelim. İsterseniz içini siz bu şekilde doldurup test edebilirsiniz:

```
apt-get update
apt-get install -y docker.io
systemctl start docker
docker run hello-world
touch win8.txt
touc win9.txt
docker ps -a
uname -a
ps aux
lsblk
ls -l
ls /
```
## Şimdi bu dosyayı github repomuza pushlayalım

Bütün Git aşamalarını bu repodan takip edebilirsiniz 
```
https://github.com/AlperRehaYAZGAN/bulut-bilisimciler-senaryolar/tree/master/git
```

```
git init
git add history.txt
git config --global user.name "GitHub Kullanıcı Adınız"
git config --global user.email "GitHub E-Posta Adresiniz"
git commit -m "first commit"
git remote add origin https://<username>:<git_user_token>@github.com/<username>/<project_name>.git
git push -u origin master
```
