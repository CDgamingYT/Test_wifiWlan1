import subprocess

def get_saved_wifi_passwords():
    networks = subprocess.check_output("netsh wlan show profiles", shell=True).decode("utf-8", errors="ignore").split('\n')
    networks = [line.split(":")[1].strip() for line in networks if "All User Profile" in line]

    for network in networks:
        try:
            result = subprocess.check_output(f'netsh wlan show profile "{network}" key=clear', shell=True).decode("utf-8", errors="ignore")
            password_line = [line.split(":")[1].strip() for line in result.split('\n') if "Key Content" in line]
            password = password_line[0] if password_line else "No password saved"
            print(f"SSID: {network}, Password: {password}")
        except Exception as e:
            print(f"Could not retrieve password for {network}: {e}")

get_saved_wifi_passwords()
