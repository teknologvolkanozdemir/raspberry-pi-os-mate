# Raspberry Pi OS üzerine MATE kurulumu

Bu kılavuz, Raspberry Pi OS çalışan bir Raspberry Pi'ye MATE masaüstü ortamını kurar. Kurulum için internet bağlantısı ve yönetici yetkisi gerekir. Komutları terminalde sırayla çalıştırın.

## 1. Sistemi güncelleyin

```bash
sudo apt update
sudo apt full-upgrade -y
```

Güncelleme tamamlandıktan sonra, çekirdek veya sistem bileşenleri güncellendiyse yeniden başlatın:

```bash
sudo reboot
```

Yeniden başladıktan sonra terminali tekrar açın.

## 2. MATE masaüstünü ve giriş yöneticisini kurun

```bash
sudo apt install mate-desktop-environment lightdm lightdm-gtk-greeter -y
```

Kurulum sırasında varsayılan görüntü yöneticisini seçmeniz istenirse **lightdm**'yi seçin. Seçim ekranı çıkmazsa LightDM'yi varsayılan yapmak için:

```bash
sudo dpkg-reconfigure lightdm
```

Açılan listeden **lightdm**'yi seçin.

İsteğe bağlı MATE uygulamalarını da kurmak isterseniz:

```bash
sudo apt install mate-desktop-environment-extras -y
```

## 3. Masaüstü açılışını ayarlayın

Raspberry Pi'yi grafik masaüstünde başlatmak için yapılandırma aracını açın:

```bash
sudo raspi-config
```

Menüde **System Options** → **Boot / Auto Login** → **Desktop** veya **Desktop Autologin** seçeneğini seçin. Menü adları Raspberry Pi OS sürümüne göre değişebilir. Otomatik oturum açma istemiyorsanız **Desktop** seçeneğini tercih edin. Ardından **Finish** ile çıkın.

## 4. Yeniden başlatın ve MATE oturumu açın

```bash
sudo reboot
```

Giriş ekranı gelirse kullanıcı hesabınızı seçin. Oturum seçici (dişli simgesi) görünüyorsa **MATE** oturumunu seçip giriş yapın.

## 5. Kurulumu doğrulayın

MATE oturumunda bir terminal açıp şu komutu çalıştırın:

```bash
echo "$XDG_CURRENT_DESKTOP"
```

Çıktıda `MATE` görüyorsanız MATE oturumu çalışıyor demektir. Kurulu MATE sürümünü görmek için:

```bash
mate-session --version
```

## Sorun giderme

- MATE görünmüyorsa oturumu kapatın ve giriş ekranındaki oturum seçicisinden **MATE**'yi seçin.
- `mate-desktop-environment` paketi bulunamıyorsa önce `sudo apt update` çalıştırın ve Raspberry Pi OS yazılım kaynaklarınızın etkin olduğundan emin olun.
- Sistem açıldığında masaüstü yerine terminal geliyorsa `sudo raspi-config` içinden masaüstü açılış seçeneğini yeniden ayarlayın.
