# Create a mime type for fritzing schematics files

Once you have installed fritzing:

        # apt get install fritzing

1. install the mime type

        $ xdg-mime install tools/fritzing-mime.xml

2. install the associated icon

        $ xdg-icon-resource install --context mimetypes --size 32 \
                /usr/share/pixmaps/fritzing_icon.xpm application/x-fritzing

3. associate .fzz files with the fritzing application

        $ xdg-mime default fritzing.desktop application/x-fritzing
        # sed -i 's/Exec=Fritzing$/Exec=Fritzing %U/' \
                /usr/share/applications/fritzing.desktop

## License

    This is part of the Carino project documentation.
    Copyright (C) 2015
      Nicolas CARRIER
    See the file doc/README.md for copying conditions
