A theme for nginx file server, using [fancyindex](https://github.com/aperezdc/ngx-fancyindex). It is modified from [this repo](https://github.com/Naereen/Nginx-Fancyindex-Theme),
See the preview [here](https://r.kingway.fun/k2/files).

## Install fancyindex module

```
sudo apt-get install -y nginx-extras
```

## Deploy theme

```
# Clone theme (for example to home/deploy directory)

cd /home/deploy
git clone https://github.com/pkufool/nginx-theme.git

# Add following lines to nginx server block

# Note the path MUST be `theme`, if you change this path, you should change the js/css path
# in header.html / footer.html accordingingly.
location /theme {
   alias /home/deploy/nginx-theme;
   try_files $uri $uri/ = 404;
}

```

## Use the theme

For each subdirectory you want to serve as file server, add following lines to its block.

```
location ^~/k2/files {
    alias /nfs/nfs1/deploy/ngk;
    fancyindex on;
    fancyindex_localtime on;
    fancyindex_name_length 255; # Maximum file name length in bytes, change as you like.
    fancyindex_exact_size off;
    fancyindex_header "/theme/header.html";
    fancyindex_footer "/theme/footer.html";
}

```

## Customized header and readme

Put a `HEADER.md` and / or `README.md` in whatever directory you want to use a customized header and/or readme.

For example, you are serving `~/example` and you put a `HEADER.md` in `~/example`, then when you navigate to `https://www.yoursize.com/example`
you can see a customized header (the content is from `HEADER.md`).  If you have a subdirectory `~/example/sub` and you add another `HEADER.md` in `~/example/sub`,
then when you navigate to `https://www.yoursize.com/example/sub` you can have a different header (the content is from `HEADER.md` in `~/example/sub`).


## Customized the footer

At the bottom there is a line with smaller characters saying that "This page is maintain by ....", you can change this line to your own style.
Open footer.html with any editor and change the content in `<footer> ... </footer>`.
