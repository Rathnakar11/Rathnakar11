
import requests

# Replace 'YOUR_API_KEY' and 'https://api.udo.com/upload_song' with actual values from Udo's API documentation
API_KEY = 'YOUR_API_KEY'
UPLOAD_URL = 'https://api.udo.com/upload_song'

def upload_song(song_name, file_path):
    headers = {
        'Authorization': f'Bearer {API_KEY}',
        'Content-Type': 'audio/mpeg'
    }
    try:
        with open(file_path, 'rb') as f:
            files = {
                'song_name': (None, song_name),
                'file': (song_name, f, 'audio/mpeg')
            }
            response = requests.post(UPLOAD_URL, headers=headers, files=files)
            if response.status_code == 200:
                print(f'Successfully uploaded {song_name}')
            else:
                print(f'Failed to upload {song_name}. Status code: {response.status_code}')
                print(response.text)
    except FileNotFoundError:
        print(f'File not found: {file_path}')
    except Exception as e:
        print(f'An error occurred: {str(e)}')

# Example usage:
song_name = 'MySong.mp3'
file_path = '/path/to/MySong.mp3'
upload_song(song_name, file_path)
