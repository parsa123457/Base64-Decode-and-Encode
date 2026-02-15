
"""
Base64 Encoder / Decoder – interactive console utility
Author: pbm 
"""

import base64
import sys
import textwrap

# -----------------
BANNER = r'''
                ..                        
              . uW8"                          
 .d``         `t888          ..    .     :    
 @8Ne.   .u    8888   .    .888: x888  x888.  
 %8888:u@88N   9888.z88N  ~`8888~'888X`?888f` 
  `888I  888.  9888  888E   X888  888X '888>  
   888I  888I  9888  888E   X888  888X '888>  
   888I  888I  9888  888E   X888  888X '888>  
 uW888L  888'  9888  888E   X888  888X '888>  
'*88888Nu88P  .8888  888"  "*88%""*88" '888!` 
~ '88888F`     `%888*%"      `~    "    `"`   
   888 ^          "`                          
   *8E                                        
   '8>                                        
    "                                         
   Base64 Encode • Decode Utility
'''
# ---------------------


def print_banner():
    """Print the banner with a thin separator."""
    print(BANNER)
    print('-' * 60)
def decode_base64(encoded_str: str) -> str:
    """
    Decode a Base64 string to UTF‑8 text.
    Returns the decoded string or raises a ValueError on failure.
    """
    try:
        padded = encoded_str.strip()
        missing_padding = len(padded) % 4
        if missing_padding:
         padded += '=' * (4 - missing_padding)
        decoded_bytes = base64.b64decode(padded, validate=True)
        return decoded_bytes.decode('utf-8')
    except Exception as exc:
        raise ValueError(f'Invalid Base64 input: {exc}')
def encode_base64(plain_str: str) -> str:
    """
    Encode a UTF‑8 string into Base64.
    Returns the Base64 representation.
    """
    encoded_bytes = base64.b64encode(plain_str.encode('utf-8'))
    return encoded_bytes.decode('utf-8')
def prompt_choice() -> str:
    """Show the menu and return the user's choice."""
    menu = textwrap.dedent("""\
        Choose an option:
        [1] Decode Base64 → Plain text
        [2] Encode plain text → Base64
        [Q] Quit
        > """)
    return input(menu).strip().lower()
def main():
    print_banner()
    while True:
        choice = prompt_choice()
        if choice == '1':
            b64_input = input('\nEnter the Base64 string to decode:\n> ').strip()
            try:
                result = decode_base64(b64_input)
                print('\nDecoded text:')
                print(result)
            except ValueError as e:
                print(f'\nError: {e}')
        elif choice == '2':
            plain_input = input('\nEnter the text you want to encode:\n> ')
            result = encode_base64(plain_input)
            print('\nBase64 output:')
            print(result)
        elif choice in ('q', 'quit', 'exit'):
            print('\nGood luck Stay safe out there.')
            sys.exit(0)
        else:
            print('\n  Invalid selection – please choose 1, 2, or Q.')
if __name__ == '__main__':
    main()
