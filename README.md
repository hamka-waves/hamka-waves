import time
import random
from telethon import TelegramClient

api_id = 'Your_Id'
api_hash = 'Your_Api'
phone_number = 'Your_Number_Phone_registered'

client = TelegramClient('bot_session', api_id, api_hash)

async def send_spam_message(usernames, message, max_messages=10):
    async with client:
        message_count = 0  
        while message_count < max_messages: 
            for username in usernames:
                if message_count >= max_messages:
                    break 
                
                try:
                    await client.send_message(username, message)
                    message_count += 1
                    print(f"Message {message_count} sent to {username}")
                except Exception as e:
                    print(f"Error sending message to {username}: {e}")
            
            delay = random.randint(10, 30)
            print(f"Waiting for {delay} seconds before sending the next message...")
            time.sleep(delay)
        
        print("Finished sending messages.")

usernames = ['@user_target']
message = "This example massage"

client.loop.run_until_complete(send_spam_message(usernames, message, max_messages=5))
