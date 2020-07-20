# Vagrant CheatSheet

### Vagrant nedir?
Vagrant bir sanal makine oluşturma aracıdır ve Vagrantfile adında bir konfigürasyon dosyasına talimatlar verilerek istenilen sanal makineyi çok kısa bir süre içerisinde çalışır duruma getirebilmektedir. 
    
Takımlar arası çalışma ortamı farklılıklarını gidermek için veya localde çalıştırılan bir programların, sunucuda çalışmaması gibi olumsuz durumları önlemek amacıyla; aynı konfigürasyonlarla aynı çalışma ortamlarını oluşturulabilmektedir.
    
### Kurulumu
> sudo apt-get install vagrant

### Centos makinesi hazırlama ve çalıştırma
Vagrant sisteminde daha önceden hazırlanmış, box adındaki paketler bulunmaktadır. Bu box adı verilen paketler kullanılarak sistemler oluşturulmaktadır. İlk örnek olarak vagrant init komutuyla, Vagrantfile adındaki dosya oluşturulmaktadır.

> vagrant init centos/7

Ardından aşağıdaki vagrant up komutuyla sanal makinenin çalışması sağlanmaktadır.

> vagrant up 

Böylece saniyeler içerisinde sanal makinemiz kullanıma hazır olmuştur.

### Sanal makine uykuya alma, uyandırma, kapatma ve kaldırma
Sanal makine kapatmak için

> vagrant halt

Sanal makine kaldırmak için

> vagrant destroy -f

Sanal makine yeniden başlatmak için

> vagrant reload

Sanal makine uyguya almak için

> vagrant suspend

Sanal makine uyandırmak için

> vagrant resume
