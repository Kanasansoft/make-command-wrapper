#!/bin/sh

if [ $# -ne 2 ] ; then
    echo "make-command-wrapper: This makes the application that wraps the shell command."
    echo "usage: make-command-wrapper [new application name] [shell command]"
    exit 1
fi

app_name="$1.app"
shell_command=$2

if [ -e "$app_name" ] ; then
    echo "The file of the same name or the folder already exists."
    exit 1
fi

mkdir $app_name
cd $app_name
mkdir Contents
cd Contents

cat <<__END_OF_MESSAGE__ >>Info.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>CFBundleExecutable</key>
    <string>core.sh</string>
    <key>CFBundlePackageType</key>
    <string>APPL</string>
    <key>CFBundleSignature</key>
    <string>????</string>
  </dict>
</plist>
__END_OF_MESSAGE__

mkdir MacOS
cd MacOS

{
  echo "#!/bin/sh"
  echo ""
  echo "$shell_command &"
  echo "exit 0"
} >>core.sh

chmod 755 core.sh

exit 0
