## Python-library-assignment: Ubuntu-Inspired Image Fetcher Assignment

# Answer
import os
import requests
from urllib.parse import urlsplit

def get_filename_from_url(url):
    """Extract filename from URL, generate default if unavailable."""
    url_path = urlsplit(url).path
    filename = os.path.basename(url_path)
    
    if not filename or '.' not in filename:
        filename = "downloaded_image.jpg"
    
    return filename

def download_image_ubuntu():
    """Download image following Ubuntu principles of community and sharing."""
    # Get URL from user
    url = input("Please enter the image URL: ").strip()
    
    if not url:
        print("No URL provided. Operation cancelled.")
        return
    
    # Create directory respectfully
    os.makedirs("Fetched_Images", exist_ok=True)
    
    try:
        # Connect to community resource
        response = requests.get(url, stream=True)
        response.raise_for_status()  # Respectful error checking
        
        # Get appropriate filename
        filename = get_filename_from_url(url)
        filepath = os.path.join("Fetched_Images", filename)
        
        # Save resource for sharing
        with open(filepath, 'wb') as f:
            for chunk in response.iter_content(chunk_size=8192):
                f.write(chunk)
        
        print(f"Image successfully downloaded and saved as: {filepath}")
        print("Thank you for sharing with the community!")
        
    except requests.exceptions.RequestException as e:
        # Graceful error handling
        print(f"Could not retrieve image: {e}")
    except IOError as e:
        print(f"Could not save image: {e}")

if __name__ == "__main__":
    download_image_ubuntu()
