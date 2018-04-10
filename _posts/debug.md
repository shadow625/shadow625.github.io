[shadow@wang ]~ $ brew install opencv3
Error: /usr/local/Cellar is not writable. You should change the
ownership and permissions of /usr/local/Cellar back to your
user account:
  sudo chown -R $(whoami) /usr/local/Cellar
Error: Cannot write to /usr/local/Cellar



sudo chmod -R 733 /usr/local/