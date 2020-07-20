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
