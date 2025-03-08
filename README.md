# Lab-Task
import platform
from abc import ABC, abstractmethod
  
class Button(ABC):
    @abstractmethod
    def render(self):
        """Each platform will have its own button rendering"""
        pass

class TextField(ABC):
    @abstractmethod
    def render(self):
        """Each platform will have its own text field rendering"""
        pass

class UIFactory(ABC):
    @abstractmethod
    def create_button(self) -> Button:
        """Create a button based on the OS"""
        pass

    @abstractmethod
    def create_text_field(self) -> TextField:
        """Create a text field based on the OS"""
        pass

class WindowsButton(Button):
    def render(self):
        print("Rendering a Windows-style Button")

class WindowsTextField(TextField):
    def render(self):
        print("Rendering a Windows-style Text Field")

class MacButton(Button):
    def render(self):
        print("Rendering a Mac-style Button")

class MacTextField(TextField):
    def render(self):
        print("Rendering a Mac-style Text Field")

class LinuxButton(Button):
    def render(self):
        print("Rendering a Linux-style Button")

class LinuxTextField(TextField):
    def render(self):
        print("Rendering a Linux-style Text Field")

class WindowsFactory(UIFactory):
    def create_button(self) -> Button:
        return WindowsButton()

    def create_text_field(self) -> TextField:
        return WindowsTextField()

class MacFactory(UIFactory):
    def create_button(self) -> Button:
        return MacButton()

    def create_text_field(self) -> TextField:
        return MacTextField()

class LinuxFactory(UIFactory):
    def create_button(self) -> Button:
        return LinuxButton()

    def create_text_field(self) -> TextField:
        return LinuxTextField()

class UIManager:
    def __init__(self):
        """Detects the operating system and selects the appropriate factory"""
        self.factory = self.get_factory()

    def get_factory(self) -> UIFactory:
        """Returns the correct factory based on the operating system"""
        os_name = platform.system()
        print(f"Detected OS: {os_name}")

        if os_name == "Windows":
            return WindowsFactory()
        elif os_name == "Darwin":
            return MacFactory()
        elif os_name == "Linux":
            return LinuxFactory()
        else:
            raise ValueError("Unsupported OS: Unable to create UI elements.")

    def create_ui(self):
        """Creates UI elements dynamically based on the OS"""
        button = self.factory.create_button()
        text_field = self.factory.create_text_field()

        button.render()
        text_field.render()

if __name__ == "__main__":
    print("Welcome to the Cross-Platform UI Framework!")
    ui_manager = UIManager()
    ui_manager.create_ui()

    OUTPUT Of This:

Welcome to the Cross-Platform UI Framework!
Detected OS: Windows
Rendering a Windows-style Button
Rendering a Windows-style Text Field
