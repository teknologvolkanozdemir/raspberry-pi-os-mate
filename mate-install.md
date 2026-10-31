Bu kılavuz, Raspberry Pi OS (ARM64) üzerinde MATE masaüstü ortamını, Wayland'den X11'e geçiş yapılandırmalarını, erişilebilirlik paketlerini, Chromium tarayıcısını ve Pi-Apps uygulama mağazasını eksiksiz şekilde kurar.

---

## 1. Sistemi Güncelleyin

```bash
sudo apt update
sudo apt full-upgrade -y

```

Güncelleme sonrası çekirdek veya sistem bileşenleri güncellendiyse cihazı yeniden başlatın:

```bash
sudo reboot

```

---

## 2. MATE Masaüstü ve Erişilebilirlik Paketlerini Kurun

MATE ortamını, ek araçları ve Orca ekran okuyucusu dahil tüm erişilebilirlik paketlerini yükleyin:

```bash
sudo apt install mate-desktop-environment mate-desktop-environment-extras orca at-spi2-core mate-accessibility-themes lightdm lightdm-gtk-greeter -y

```

Kurulum sırasında görüntü yöneticisi sorulursa **lightdm** seçeneğini belirleyin.

---

## 3. Ekran Sunucusunu X11 Olarak Ayarlayın

MATE masaüstü ortamı X11 altyapısıyla stabil çalıştığı için varsayılan Wayland sunucusunu X11'e çekmek gereklidir:

1. Terminalde `sudo raspi-config` komutunu çalıştırın.


2. **Advanced Options** menüsüne girin.


3. **Wayland** seçeneğini bulun.


4. **W1 X11** seçeneğini işaretleyip **OK** deyin.


5. **Finish** ile çıkın. Yeniden başlatma sorulduğunda şimdilik **No** deyin.



---

## 4. Varsayılan Oturum Yöneticisini MATE Olarak Seçin

Sistemin açılışta MATE oturumunu yüklemesi için şu komutu çalıştırın:

```bash
sudo update-alternatives --config x-session-manager

```

Listede `mate-session` satırının başındaki numarayı yazıp **Enter** tuşuna basın.

---

## 5. Kullanıcı Oturumu ve LightDM Yapılandırmasını Sabitleyin

Sistemin varsayılan PIXEL oturumuna geri dönmesini engellemek için oturum ayarlarını yapın:

```bash
echo "mate-session" > ~/.xsession
chmod +x ~/.xsession

sudo sed -i 's/^user-session=.*/user-session=mate/' /etc/lightdm/lightdm.conf
echo -e "[Seat:*]\nuser-session=mate" | sudo tee /etc/lightdm/lightdm.conf.d/99-mate.conf
sudo sed -i 's/autologin-session=.*/autologin-session=mate/' /etc/lightdm/lightdm.conf

```

---

## 6. Google Chrome (Chromium ARM64) Kurulumu

Google, Linux için tescilli `.deb` paketini yalnızca x86_64 mimarisine sunduğundan; ARM64 Linux üzerinde Google Chrome deneyimi, Chrome ile tamamen aynı altyapıyı paylaşan Chromium ARM64 sürümü ile sağlanır.

```bash
sudo apt install chromium-browser chromium-browser-l10n -y

```

---

## 7. Pi-Apps Kurulumu

Raspberry Pi OS için açık kaynaklı uygulama mağazası olan Pi-Apps'i kurmak için şu komutu çalıştırın:

```bash
wget -qO- https://raw.githubusercontent.com/Botspot/pi-apps/master/install | bash

```

---

## 8. Sistemi Yeniden Başlatın ve Doğrulayın

Tüm ayarların devreye girmesi için sistemi yeniden başlatın:

```bash
sudo reboot

```

Sistem açıldığında doğrudan MATE masaüstü yüklenecektir. Oturumu doğrulamak için terminalde şu komutu çalıştırabilirsiniz:

```bash
echo "$XDG_CURRENT_DESKTOP"

```

Çıktıda `MATE` görünüyorsa kurulum başarıyla tamamlanmıştır.
