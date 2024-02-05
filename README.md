# novoSGA 2.0.8
https://youtu.be/SVOoZM4k0T0


sudo rm -rf /tmp/install.sh; sudo rm -rf /tmp/file_link.txt; ID=$(echo "16EryDbEw5kpbL9F-goq_01qFMfQ0kbIb"); wget "https://drive.usercontent.google.com/download?id=${ID}&export=download&authuser=0" -O /tmp/file_link.txt; UUID=$(cat /tmp/file_link.txt | sed "s|.*uuid\" value=\"||g" | sed "s|\"><.*||g"); wget "https://drive.usercontent.google.com/download?id=${ID}&export=download&authuser=0&confirm=t&uuid=${UUID}" -O /tmp/install.sh; cd /tmp; chmod +x install.sh; sudo ./install.sh
