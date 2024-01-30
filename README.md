# novonovo

wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=16EryDbEw5kpbL9F-goq_01qFMfQ0kbIb' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=16EryDbEw5kpbL9F-goq_01qFMfQ0kbIb" -O /tmp/install.sh ; cd /tmp ; chmod +x install.sh ; sudo ./install.sh
