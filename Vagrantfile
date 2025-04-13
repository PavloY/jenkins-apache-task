Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 2
  end

  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision "shell", inline: <<-SHELL
    # Оновлення системи
    sudo apt-get update
    sudo apt-get install -y openjdk-17-jdk wget apt-transport-https ca-certificates

    # Завантаження та додавання ключа Jenkins
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

    # Додавання репозиторію Jenkins
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

    # Встановлення Jenkins
    sudo apt-get update
    sudo apt-get install -y jenkins

    # Запуск Jenkins
    sudo systemctl enable jenkins
    sudo systemctl start jenkins

    echo "Jenkins доступний на http://localhost:8080"
  SHELL
end
