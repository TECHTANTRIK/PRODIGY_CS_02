# PRODIGY_CS_02
image manipulation tool (using python)
here'a a image manipulation tool where you can encrypt or decrypt your image by shuffling image pixels and using operations.
============================code========================================================================================
from PIL import Image
import numpy as np
import sys

def encrypt_image(input_path, output_path, key):
    """Encrypt an image by modifying its pixel values."""
    try:
        image = Image.open(input_path)  # Use the passed input path
        pixel_array = np.array(image)

        # Encrypt by adding the key to each pixel value
        encrypted_array = (pixel_array + key) % 256

        encrypted_image = Image.fromarray(np.uint8(encrypted_array))
        encrypted_image.save(output_path)  # Save to the passed output path
        print(f"Image encrypted and saved to {output_path}")
    except Exception as e:
        print(f"Error encrypting the image: {e}")

def decrypt_image(input_path, output_path, key):
    """Decrypt an image by reversing the encryption process."""
    try:
        image = Image.open(input_path)
        pixel_array = np.array(image)

        # Decrypt by subtracting the key from each pixel value
        decrypted_array = (pixel_array - key) % 256

        decrypted_image = Image.fromarray(np.uint8(decrypted_array))
        decrypted_image.save(output_path)
        print(f"Image decrypted and saved to {output_path}")
    except Exception as e:
        print(f"Error decrypting the image: {e}")

def main():
    if len(sys.argv) < 5:
        print("Usage: python image_encryption_tool.py <encrypt/decrypt> <input_path> <output_path> <key>")
        return

    operation = sys.argv[1].lower()
    input_path = sys.argv[2]
    output_path = sys.argv[3]
    try:
        key = int(sys.argv[4])
    except ValueError:
        print("Key must be an integer.")
        return

    if operation == 'encrypt':
        encrypt_image(input_path, output_path, key)
    elif operation == 'decrypt':
        decrypt_image(input_path, output_path, key)
    else:
        print("Invalid operation. Use 'encrypt' or 'decrypt'.")

if __name__ == "__main__":
    main()
