## Description
**Title:** Tap Secrets  
**Author:** Suraj  
**Points:** 300 

You’ve been provided with filtered call logs from the CEO, which contain suspicious long numbers suggesting covert communications. These entries may unveil a hidden conspiracy within WindShine Pvt. Ltd.

---

## Writeup
1. **Analyze the Logs**:  
   The logs included fields such as Date, Time, Call Type, Status, Duration, and the critical "Number Dialed" field. This field contained sequences like `7 666 0 33 777 8 8 8 3 8 0`, resembling old mobile multi-tap SMS encoding.

2. **Identify Encoding Pattern**:  
   Each digit (2–9) could correspond to letters, much like a phone keypad. For instance, `2` represents "ABC," `3` for "DEF," and so on. Spaces (`0`) in the sequence indicated gaps between words.

3. **Develop a Decoding Script**:  
   Use the following Python script to decode the sequences:

   ```python
    import csv

    char_mapping = {
        '2': 'A',
        '22': 'B',
        '222': 'C',
        '3': 'D',
        '33': 'E',
        '333': 'F',
        '4': 'G',
        '44': 'H',
        '444': 'I',
        '5': 'J',
        '55': 'K',
        '555': 'L',
        '6': 'M',
        '66': 'N',
        '666': 'O',
        '7': 'P',
        '77': 'Q',
        '777': 'R',
        '7777': 'S',
        '8': 'T',
        '88': 'U',
        '888': 'V',
        '9': 'W',
        '99': 'X',
        '999': 'Y',
        '9999': 'Z',
        '0': ' '
    }

    def decode_message(encoded_message):
        encoded_numbers = encoded_message.split()
        
        decoded_message = ''.join(char_mapping.get(num, '') for num in encoded_numbers)
        
        return decoded_message

    csv_file_path = 'suspicious_call_log.csv'

    with open(csv_file_path, mode='r') as file:
        reader = csv.DictReader(file)
        for row in reader:
            encoded_numbers = row['Number Dialed']
            decoded_message = decode_message(encoded_numbers)
            print(decoded_message)
