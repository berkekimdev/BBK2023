# history.txt Dosyasının Yeni Sunucuya Aktarılması

### Kullanıcının Git Repository'sini Çekmesi

Aşağıda verilen komutu kullanarak oluşturmuş olduğunuz repository'inizi çekiniz.

```
git clone https://<username>:<git_user_token>@github.com/<username>/<project_name>.git
```

### myscript.sh dosyasının çalıştırılması
Çektiğiniz history.txt dosyasının olduğu directory'de myscript.sh diye bir file oluşturunuz. 

 ```
#!/bin/bash

while IFS= read -r line; do
    while true; do
        echo "Çalıştırmak istiyor musunuz? $line (E/H)"
        read -r answer </dev/tty
        case $answer in
            [eE])
                echo "Çalıştırılıyor: $line"
                eval "$line"
                if [ $? -eq 0 ]; then
                    break
                else
                    while true; do
                        read -r -p "Hata oluştu: $line. Yanlış girişi düzeltmek ister misiniz? (Y/N): " retry </dev/tty
                        case $retry in
                            [yY])
                                read -r -p "Yeni girişi yapın: " new_input </dev/tty
                                line="$new_input"
                                break
                                ;;
                            [nN])
                                break 2
                                ;;
                            *)
                                echo "Geçersiz yanıt. Y veya N girin."
                                ;;
                        esac
                    done
                fi
                ;;
            [hH])
                break
                ;;
            *)
                break
                ;;
        esac
    done
done < history.txt
 ```
Dosyayı oluşturduktan sonra gerekli execute iznini verip çalıştıralım.

```
chmod +x myscript.sh
./myscript.sh
```

Bu işlemden sonra eski komutlarımızdan hangisini bize çalıştırmak istediğimizi tek tek soracak. Hatalı bir komut yazdıysanız doğrusunu yazmanız için size input verecektir.