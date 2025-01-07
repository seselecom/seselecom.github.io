# Import necessary libraries
from html.parser import HTMLParser
from urllib.request import urlopen

# HTMLValidator class for error checking
class HTMLValidator(HTMLParser):
    def __init__(self):
        super().__init__()
        self.errors = []

    def handle_starttag(self, tag, attrs):
        # Track all tags
        pass

    def handle_endtag(self, tag):
        # Track all closing tags
        pass

    def handle_startendtag(self, tag, attrs):
        # Track self-closing tags
        pass

    def handle_data(self, data):
        # Handle raw text (can be checked later for some potential issues)
        pass

    def error(self, message):
        # Collect errors for the report
        self.errors.append(message)

    def validate_html(self, html_content):
        try:
            self.feed(html_content)
        except Exception as e:
            return f"Error while parsing: {e}"

        if not self.errors:
            return "HTML is valid!"
        else:
            return "\n".join(self.errors)

# Testing HTML file
def check_html_file(file_path):
    with open(file_path, 'r') as file:
        html_content = file.read()

    validator = HTMLValidator()
    result = validator.validate_html(html_content)
    return result

# Example: Check HTML file located in Colab
file_path = 'https://seselecom.github.io'  # Replace with your actual file path
validation_result = check_html_file(file_path)
print(validation_result)
