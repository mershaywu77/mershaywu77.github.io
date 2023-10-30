On Ubuntu Server host execute these commands :
sudo chmod -R 777 /path-to-shared-folder/shared-folder
sudo chown -R user1:user1 /path-to-shared-folder/shared-folder  
On Lubuntu Desktop guest execute this command :
sudo usermod -G vboxsf -a user2
Restart the guest system for changes taking effect.
Note : user1 = your host user name | user2 = your guest user name

From <https://askubuntu.com/questions/747974/virtualbox-shared-folders-are-owned-by-root-in-lubuntu-guest> 