import subprocess
import logging
from datetime import datetime

# Configure logging
logging.basicConfig(filename='backup.log', level=logging.INFO, 
                    format='%(asctime)s - %(levelname)s - %(message)s')

# Define the source directory and remote details
SOURCE_DIR = '/path/to/source/directory/'
REMOTE_USER = 'your_username'
REMOTE_SERVER = 'remote.server.com'
REMOTE_DIR = '/path/to/remote/backup/directory/'

def backup_directory(source_dir, remote_user, remote_server, remote_dir):
    try:
        result = subprocess.run(
            ['rsync', '-avz', source_dir, f'{remote_user}@{remote_server}:{remote_dir}'],
            check=True,
            capture_output=True,
            text=True
        )
        report_success(source_dir, remote_dir)
    except subprocess.CalledProcessError as e:
        report_failure(source_dir, remote_dir, e.stderr)

def report_success(source, destination):
    message = f"Backup successful: {source} to {destination}"
    print(message)
    logging.info(message)

def report_failure(source, destination, error):
    message = f"Backup failed: {source} to {destination}. Error: {error}"
    print(message)
    logging.error(message)

def main():
    print("Starting backup process...")
    backup_directory(SOURCE_DIR, REMOTE_USER, REMOTE_SERVER, REMOTE_DIR)

if __name__ == "__main__":
    main()
