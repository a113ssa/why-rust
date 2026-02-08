# Why Rust
## Embedded

<details>
  <summary><h3>Typestate Pattern</h3></summary>

**Case**: Imagine you are programming a microcontroller (like an STM32 or nRF52). You have a GPIO pin.<br><br>
**In C**:<br>
You configure a pin as an "Output." Later in the code, due to a copy-paste error or a logic bug, you accidentally try to read from that pin as if it were an "Input."<br>
**Result**: The code compiles. The processor runs. It might return garbage data, or in some hardware configurations, it might physically damage the chip (short circuit).<br><br>
**In Embedded Rust**:<br>
Rust uses **"Typestate"** to prevent this.
- When you start, the pin is a generic type, e.g., Pin<Disconnected>.</li>
- You call a function to turn it into an output: <code>let output_pin = pin.into_push_pull_output();</code></li>
- Here is the magic: The original variable pin is consumed (moved). It no longer exists. You now possess a variable of type Pin<Output>.</li>
- The Pin<Output> type has a method called <code>set_high()</code>., but it does not have a method called <code>.read().</code></li>
- If you try to type output_pin.read(), the code will not compile.</li>

</details> 
