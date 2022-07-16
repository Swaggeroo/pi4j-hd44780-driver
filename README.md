# HD44780 LCD driver for pi4J

This driver supports LCD peripherals built on the HD44780 chip and controlled with the PCF8574 chip.

NOTE: these drivers are not production-ready. There is no guarantee
of correctness, completeness or robustness. Its only testet for a 16x2 LCD!

This driver is based on the [lcd-pcf8574-androidthings driver from Nilhcem](https://github.com/Nilhcem/lcd-pcf8574-androidthings)
and the [hd44780-i2c driver from gorskima](https://github.com/gorskima/hd44780-i2c) and the [hd44780-i2c androidthings-drivers from leinardi](https://github.com/leinardi/androidthings-drivers)

## How to use the driver

### Dependencies

Java 11 or higher is required.

````xml
    <dependencies>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.36</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.36</version>
        </dependency>


        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-core</artifactId>
            <version>2.1.1</version>
            <scope>compile</scope>
        </dependency>

        <!-- include Pi4J Plugins (Platforms and I/O Providers) -->
        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-plugin-raspberrypi</artifactId>
            <version>2.1.1</version>
        </dependency>
        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-plugin-pigpio</artifactId>
            <version>2.1.1</version>
        </dependency>
        <dependency>
            <groupId>com.pi4j</groupId>
            <artifactId>pi4j-plugin-linuxfs</artifactId>
            <version>2.1.1</version>
        </dependency>
    </dependencies>

    <!-- DEPENDENCY REPOSITORIES -->
    <repositories>
        <repository>
            <id>oss-snapshots-repo</id>
            <name>Sonatype OSS Maven Repository</name>
            <url>https://oss.sonatype.org/content/groups/public</url>
            <releases>
                <enabled>false</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>
````

### Sample usage

Just Copy the java-file in our project.

```java

// Access the LCD:
Hd44780 mLcd;

try {
    mLcd = new Hd44780(1,0x27, Hd44780.LCD_16X2);
} catch (IOException e) {
    // couldn't configure the LCD...
}

// Draw on the screen:

try {
     mLcd.setBacklight(true);
     mLcd.cursorHome();
     mLcd.clearDisplay();
     mLcd.setText("Hello LCD");
     int[] heart = {0b00000, 0b01010, 0b11111, 0b11111, 0b11111, 0b01110, 0b00100, 0b00000};
     mLcd.createCustomChar(heart, 0);
     mLcd.setCursor(10, 0);
     mLcd.writeCustomChar(0);
} catch (IOException e) {
    // error setting LCD
}

// Close the LCD when finished:

try {
    mLcd.close();
} catch (IOException e) {
    // error closing LCD
}
```
