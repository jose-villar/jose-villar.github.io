# Tendencias en Tecnologías Computacionales

## Arduinos

- Push buttons connect terminals on the same line; when they're pushed, they
  connect to the parallel terminals.

### LED

- LEDs have direction. The long leg connects to the voltage and the short leg
  connects to the ground.

### Resistors

- Note that voltage drops across resistors when current is flowing.

- Pull up resistors: 5V → Resistor → ReadPin → Switch → Ground (▽)

  - In case the switch was open, ReadPin will report a 1.

  - In case the switch was closed, ReadPin will report a 0.

- Pull down resistors: 5V → Switch → ReadPin → Resistor → Ground

  - In case the switch was open, ReadPin will report a 0.

  - In case the switch was closed, ReadPin will report a 1.

- Note: Digital read reports the electrical potencial, not the voltage.
