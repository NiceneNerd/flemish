# Flemish

An elmish architecture for fltk-rs.

## Usage
Add flemish to your dependencies:
```toml
[dependencies]
flemish = "0.1"
```

A usage example:
```rust
use flemish::{
    button::Button, frame::Frame, Flex, FlexType, OnEvent, Sandbox, Settings
};

pub fn main() {
    Counter::new().run(Settings {
        size: (300, 100),
        resizable: true,
        ..Default::default()
    })
}

#[derive(Default)]
struct Counter {
    value: i32,
}

#[derive(Debug, Clone, Copy)]
enum Message {
    IncrementPressed,
    DecrementPressed,
}

impl OnEvent<Message> for Button {}

impl Sandbox for Counter {
    type Message = Message;

    fn new() -> Self {
        Self::default()
    }

    fn title(&self) -> String {
        String::from("Counter - fltk-rs")
    }

    fn update(&mut self, message: Message) {
        match message {
            Message::IncrementPressed => {
                self.value += 1;
            }
            Message::DecrementPressed => {
                self.value -= 1;
            }
        }
    }

    fn view(&mut self) -> Flex {
        let mut col = Flex::default().with_type(FlexType::Column);
        let mut button1 = Button::default().with_label("Increment");
        button1.on_event(Message::IncrementPressed);
        Frame::default().with_label(&self.value.to_string());
        let mut button2 = Button::default().with_label("Decrement");
        button2.on_event(Message::DecrementPressed);
        col.end();
        col
    }
}
```
