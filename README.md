# The files I use to render my json-resume

## Name of the deposit

The name of this repo follows [the Github pages recommendations](https://pages.github.com/) (if your account has uppercase letters, convert them for the repo/page name).  
That way, my resume exported as an `ìndex.html` is automatically visibile on my  [github page](https://frankwap.github.io/).  

TODO/YAGNI: add a switch to see an English version.

## install NodeJS

To install NodeJS for all users (in `/sur/local/share`):

```bash
# you can change the link as needed
njs_link=https://nodejs.org/dist/v20.10.0/node-v20.10.0-linux-x64.tar.xz
njs_file=$(basename $njs_link)
njs_name=${njs_file/.tar.xz/}
cd /tmp
wget --no-clobber $njs_link
sudo -s
tar xvf $njs_file
chmod -R 755 $njs_name
mv $njs_name  /usr/local/share/
ln -s /usr/local/share/$njs_name/bin/* /usr/local/bin/
exit
```

## install resumed and add my theme

To install resumed locally, with my forked themed:

```bash
# you can change the (global) directory as needed
resumed_dir=$HOME/resumed
test -d $resumed_dir & rm -rf $resumed_dir
cd /tmp
wget --no-clobber https://github.com/rbardini/resumed/archive/master.zip --output-document=/tmp/resumed-master.zip
unzip resumed-master.zip
mv resumed-master $resumed_dir
cd $resumed_dir
npm install resumed
# 
cd /tmp 
wget --no-clobber https://github.com/FrankwaP/jsonresume-theme-frankwap-fr/archive/master.zip --output-document=/tmp/jsonresume-theme-frankwap-fr-master.zip
unzip theme-master.zip
mv jsonresume-theme-frankwap-fr-master $resumed_dir/node_modules/jsonresume-theme-frankwap-fr
```

## Render the resume

```bash
# you can change the json file 
json=fr.json
# you can change the (global) directory as needed
resumed_dir=$HOME/resumed
theme=jsonresume-theme-frankwap-fr
resumed --help &> /dev/null || export PATH=$resumed_dir/node_modules/.bin/:$PATH
resumed validate $json && resumed render $json  --output index.html --theme $theme
```
