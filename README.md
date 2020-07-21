# Vagrant

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

### Vagrant Box oluşturma
Oluşturulan sanal makine farklı ortamlara taşınmak üzere box olarak saklanabilmektedir.

> vagrant package --output new.box

Oluşturulan box farklı ortamlarda aşağıdaki şekilde çalıştırılabilmektedir.

> vagrant box add new.box --name newbox

### Vagrant sanal makinelere erişme
Oluşturulan sanal makinelere vagrant ssh komutuyla erişilebilmektedir.

> vagrant ssh

## Vagrantfile

### Box
Vagrantfile içerisindeki konfigürasyona göre box ifadesi, sanal makine işletim sisteminin adı belirtilmektedir.
```ruby
Vagrant.configure(2) do |config|
    config.vm.box = "Centos/7"
end
```

### Provider
Vagrant yazılımının sanallaştırma işlemini yerine getiren programların tanımlandığı anahtar kelimedir. Default olarak open source olan VirtualBox kullanılmaktadır. Ayrıca farklı sanallaştırma sağlayan programlarla da; provider konfigürasyonu ile ayarlama sağlanmaktadır.
```ruby
Vagrant.configure(2) do |config|
    config.vm.box = "Centos/7"
    config.vm.provider "virtualbox" do |vb|
        # vb.gui = true
        vb.memory = "1024"
        vb.cpus = 2
    end
end
```

### Network
Vagrant ile oluşturulan sanal makinelerin haberleşmeleri ile ilgili ayarların yapılması sağlanmaktadır.
```ruby
Vagrant.configure(2) do |config|
    config.vm.box = "Centos/7"
    config.vm.network "private_network", ip: "192.168.0.10"
    # config.vm.network "forwarded_port", guest: 80, host: 8080
    # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
    # config.vm.network "public_network"
end
```

### Synced folder
Sanal makinelerdeki dosyaların paylaşılması sağlanmaktadır.
```ruby
Vagrant.configure(2) do |config|
    config.vm.box = "Centos/7"
    config.vm.synced_folder "./data", "vagrant_data"
end
```

### Provision
Sanal sunuculara gerekli yazılımların yüklenmesini sağlamaktadır. Vagrantfile ile Ansible, Chef, Puppet veya Shell script yapılandırma için kullanılabilir.
```ruby
Vagrant.configure(2) do |config|
    config.vm.box = "Centos/7"
    config.vm.provision "shell", inline: <<-SHELL
        yum install git
    SHELL
    # config.vm.provision "shell", path: "config.sh"
end
```

## Birden fazla sanal makine oluşturma
Sanal makineleri istenilen sayıda ve farklı işletim sistemleri olarak çok kısa bir zaman içerisinde oluşturabilirsiniz.
```ruby
BOX_NAME = "ubuntu/xenial64"
NODE_COUNT = 2
Vagrant.configure(2) do |config|
    config.vm.define "master" do |subconfig|
        subconfig.vm.box = BOX_IMAGE
        subconfig.vm.hostname = "master"
        subconfig.vm.network :private_network, ip: "10.0.0.10"
    end

    (1..NODE_COUNT).each do |i|
        config.vm.define "node#{i}" do |subconfig|
            subconfig.vm.box = BOX_IMAGE
            subconfig.vm.hostname = "node#{i}"
            subconfig.vm.network :private_network, ip: "10.0.0.#{i + 10}"
        end
    end
end
```
