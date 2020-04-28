================================================================================

                Pop Library Function Description for PyCBasic 

================================================================================

*********************************** Class Out **********************************

[Class Description]

    - Output device controlled throught GPIO.
    - Led(n)
        : Out Object
        [Params]
            @ n : GPIO Number Connected to the Output Device  

[Functions]

    - on()
        : Set GPIO Connected to Output Device to HIGH.]
    - off()
        : Set GPIO Connected to Output Device to LOW.

*********************************** Class Led **********************************

[Class Description]

    - LEDs are controlled via GPIO.
    - Led(n)
        : Led Object inheriting from Out Class
        [Params]
            @ n : GPIO Number Connected to the LED 

*********************************** Class Input **********************************

[Class Description]

    - Read the Input Device through GPIO.
    - Input(n,activeHigh=Ture)
        : Input Object
        [Params]
            @ n : GPIO Number Connected to the Input Device. 
            @ activeHigh : Used to check if the Input Device is HIGH when pressed , Default True.

[Defines]

    - FALLING : Detect Falling Edge 
    - RISING : Detect Rising Edge
    - BOTH : Detect Both Side 

[Functions]

    - read()
        : Read the Input Device Status. 
    - setCallback(func,param=None,type=BOTH)
        : Set Callback Function When Detect Edge.
        [Params]
            @ func : Function to use when calling Callback
            @ param : Arguments passed to the Callback function , Default None 
            @ type : Call condition of Callback function , Default BOTH

*********************************** Class Switch **********************************

[Class Description]

    - Read the switch status through GPIO.
    - Switch(n,activeHigh=Ture)
        : Switch Object inheriting from Input Class
        [Params]
            @ n : GPIO Number Connected to the Switch. 
            @ activeHigh : Used to check if the switch is HIGH when pressed , Default True.

*********************************** Class SpiAdc **********************************

[Class Description]

    - adc chip control through spi interface 
    - SpiAdc(channel, device=0, bus=0, speed=1000000)
        : SpiAdc object
        [Params]
            @ channel : ADC Channel 
            @ device : SPI Interface Channel , Default 0 (in Raspberry Pi)
            @ bus : Not Used.. 
            @ speed : SPI Interface Clock Speed , Default 1000000(1MHz)

[Defines]

    - TYPE_AVERAGE : Average data based on sampling count
    - TYPE_NORMAL : Unaveraged raw data
    - MODE_FULL : Call Callback function always*
    - MODE_INCLUSIVE : If data is in arange(max, min), call Callback function *
    - MODE_EXCLUSIVE : If data is over arange, call Callback function *

[Functions]        

    - setChipSelect(cs)
        : Set SPI Chip Select PIN 
        [Params]
            @ cs : Chipselect GPIO for SPI Interface 
    - setCallback(func,param=None,type=TYPE_AVERAGE,mode=MODE_FULL,min=0,max=ADC_MAX)
        : Set up callback function for automatic data read
        [Params]
            @ func : Function to use when calling Callback 
            @ param : Arguments passed to the Callback function , Default None 
            @ type : Data Read Type , Default TYPE_AVERAGE
            @ mode : Select Mode , Default MODE_FULL
            @ min : analog data minimum , Default 0 
            @ max : analog data maximum , Default 4095 (MCP3208 12bit ADC Chip)
    - setSample(sample)
        : Set Sampling Count
        [Params]
            @ sample : Sampling count
    - getSample()
        : Get Sampling Count 
    - read()
        : Read Data from Device (Raw Type)
    - readAverage()
        : Read Average Data from Device 
    - readVolt(ref=3.3,max=3020.0)
        : Read Data from Device (Voltage Type)
        [Params]
            @ ref : Reference Voltage 
            @ max : Maximum value of raw data
    - readVoltAverage(ref=3.3,max=3020.0)
        : Read Data from Device (Voltage Type)
        [Params]
            @ ref : Reference Voltage 
            @ max : Maximum value of raw data
    - calcDist(val,calibration=1.1) * - REMOVED
    - run() * ADDED
        : Read data and call Callback function according to mode
    
*********************************** Class PSD **********************************

[Class Description]

    - Distance measurement using PSD sensor.
    - Psd(channel, device=0, bus=0, speed=1000000)
        : PSD object inheriting from SpiAdc Class 
        [Params]
            @ channel : ADC Channel 
            @ device : SPI Interface Channel , Default 0 (in Raspberry Pi)
            @ bus : Not Used.. 
            @ speed : SPI Interface Clock Speed , Default 1000000(1MHz)

[Functions]       

    - calcDist(val,calibration=1.1)
        : Calculate distance value from raw data
        [Params]
            @ val : ADC Raw Data 
            @ calibration : Calibration Value, Default 1.1 *

*********************************** Class CDS **********************************

[Class Description]

    - Light measurement using CDS sensor.
    - Cds(channel, device=0, bus=0, speed=1000000)
        : Cds object inheriting from SpiAdc Class 
        [Params]
            @ channel : ADC Channel 
            @ device : SPI Interface Channel , Default 0 (in Raspberry Pi)
            @ bus : Not Used.. 
            @ speed : SPI Interface Clock Speed , Default 1000000(1MHz)

[Functions]        

    - setCalibrationPseudoLx(func)
        : Set calibration function
        [Params]
            @ func : Calibration function.*
    - readAverage()
        : Read average data from device and calibration function *

*********************************** Class Sound **********************************

[Class Description]

    - Ambient sound measurement using Sound sensor.
    - Sound(channel, device=0, bus=0, speed=1000000)
        : Sound object inheriting from SpiAdc Class 
        [Params]
            @ channel : ADC Channel 
            @ device : SPI Interface Channel , Default 0 (in Raspberry Pi)
            @ bus : Not Used.. 
            @ speed : SPI Interface Clock Speed , Default 1000000(1MHz)

*********************************** Class Vr **********************************

[Class Description]

    - Voltage measurement with variable resistor
    - Vr(channel, device=0, bus=0, speed=1000000)
        : Vr object inheriting from SpiAdc Class 
        [Params]
            @ channel : ADC Channel 
            @ device : SPI Interface Channel , Default 0 (in Raspberry Pi)
            @ bus : Not Used.. 
            @ speed : SPI Interface Clock Speed , Default 1000000(1MHz)

[Functions] 

    - setCalibrationPseudoLx(func)
        : Set calibration function 
        [Params]
            @ func : Calibration function
    - readAverage()
        : Read average data from device and calibration function

*********************************** Class Piezo **********************************

[Class Description]

    - Piezo controlled via Hardware PWM
    - Piezo(n)
        : Piezo object inheriting from HwPwm Class 
        [Params]
            @ n : GPIO Number Connected to the Piezo 
            (Only Use in Raspberry Pi CH0 -> D12,D18 or CH1 -> D13) 

[Functions]

    - setTempo(n)
        : Set tempo value
        [Params]  
            @ n : Value to be set to tempo
    - getTempo()
        : Get tempo value
    - tone(scale,pitch,duration)
        : Play a note on piezo buzzer during duration value
        [Params]
            @ scale : Scale value to play on piezo buzzer (int type).
            @ pitch : Pitch value to play on piezo buzzer. 'Do' is 1, 'Do♯' is 2, 'Re' is 3 and 'Si' is 12.
            @ duration : Tone is playing during duration value.
    - rest(duration)
        : Stop to play piezo buzzer.
        [Params]
            @ duration : The duration of the stopping.

*********************************** Class LedStrip **********************************

[Class Description]

    - Pixel Display controlled via Hardware PWM 
    - LedStrip(n)
        : LedStrip object inheriting from pixelbuf Class 
        [Params]
            @ n : Number of Pixel (ex 8x8 -> 64)

[Functions]

    - show()
        : Write buffer data on LED Strip
    - fill(color)
        : Fill LED Strip to one color
        [Params]
            @ color : A color to be filled. Type is list of [R, G, B]

*********************************** Class Oled **********************************

[Class Description]

    - Oled Controlled vi I2C Interface 
    - Oled()
        : Oled object inheriting from I2C Class (I2c Slave Address -> 0x3c)

[Defines]

    - OLED_SSD1306_I2C_128x32
        : OLED device type number, if model name is 'SSD1306', select this type.
    - OLED_SH1106_I2C_128x64
        : OLED device type number, if model name is 'SSH1106', select this type.
    - BLACK
        : In OLED, you can use only 2 colors. One of them is black. Numeric value is 0.
    - WHITE
        : Another of them is white. Numeric value is 1.

[Functions]

    - init(type=OLED_SH1106_I2C_128x64)
        : Initialize OLED and set width/height of OLED. This function calls setTextSize(), setTextColor(), clearDisplay()
        [Params]
            @ type : Select OLED type.
    - print(string)
        : Print a string on OLED. Replace '\n' to New-Line
        [Params]
            @ string: The string to print on OLED.
    - drawCircle(x0, y0, r, color)
        : Draw a circle on OLED
        [Params]
            @ x0 : Start point of x-axis
            @ y0 : Start point of y-axis
            @ r : Radious of the circle
            @ color : The color of a circle. BLACK(0) or WHITE(1)
    - fillCircle(x0, y0, r, color)
        : Draw a filled circle on OLED
        [Params]
            @ x0 : Start point of x-axis
            @ y0 : Start point of y-axis
            @ r : Radious of the circle
            @ color : The color of a circle. BLACK(0) or WHITE(1)
    - drawLine(x0, y0, x1, y1, color)
        : Draw a line on OLED
        [Params]
            @ x0 : Start point of x-axis
            @ y0 : Start point of y-axis
            @ x1 : End point of x-axis
            @ y1 : End point of y-axis
            @ color : The color of a line. BLACK(0) or WHITE(1)
    - drawRect(x, y, w, h, color)
        : Draw a rectangle on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ w : Width of the rectangle
            @ h : Height of the rectangle
            @ color : The color of a rectangle. BLACK(0) or WHITE(1)
    - fillRect(x, y, w, h, color)
        : Draw a filled rectangle on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ w : Width of the rectangle
            @ h : Height of the rectangle
            @ color : The color of a rectangle. BLACK(0) or WHITE(1)
    - drawVerticalBargraph(x, y, w, h, color, percent)
        : Draw a graph on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ w : Width of the graph
            @ h : Full height of the graph
            @ color : The color of the graph. BLACK(0) or WHITE(1)
            @ percent : The percentage of a graph. The direction of graph is always up-side.
    - drawHorizontalBargraph(x, y, w, h, color, percent)
        : Draw a graph on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ w : Full width of the graph
            @ h : Height of the graph
            @ color : The color of the graph. BLACK(0) or WHITE(1)
            @ percent : The percentage of a graph. The direction of graph is always right-side.
    - drawRoundRect(x, y, w, h, r, color)
        : Draw a rounded rectangle on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ w : Width of the rounded rectangle
            @ h : Height of the rounded rectangle
            @ r : Curvature of edge of the rounded rectangle
            @ color : The color of a graph. BLACK(0) or WHITE(1)
    - fillRoundRect(x, y, w, h, r, color)
        : Draw a rounded and filled rectangle on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ w : Width of the rounded rectangle
            @ h : Height of the rounded rectangle
            @ r : Curvature of edge of the rounded rectangle
            @ color : The color of a graph BLACK(0) or WHITE(1)
    - drawTriangle(x0, y0, x1, y1, x2, y2, color)
        : Draw a triangle on OLED
        [Params]
            @ x0 : First point of x-axis 
            @ y0 : First point of y-axis
            @ x1 : Second point of x-axis 
            @ y1 : Second point of y-axis
            @ x2 : Third point of x-axis 
            @ y2 : Third point of y-axis
            @ color : The color of a triangle. BLACK(0) or WHITE(1)
    - fillTriangle(x0, y0, x1, y1, x2, y2, color)
        : Draw a filled triangle on OLED
        [Params]
            @ x0 : First point of x-axis 
            @ y0 : First point of y-axis
            @ x1 : Second point of x-axis 
            @ y1 : Second point of y-axis
            @ x2 : Third point of x-axis 
            @ y2 : Third point of y-axis
            @ color : The color of a triangle. BLACK(0) or WHITE(1)
    - drawChar(x, y, c, color, bg, size)
        : Draw a character on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of x-axis
            @ c : A character to be drawn
            @ color : The color of a character. BLACK(0) or WHITE(1)
            @ bg : The background of a character. Background size is 6 * 8 * textsize
            @ size : Pixel size of charactor strock. Default is 1
    - drawBitmap(x, y, bitmap, w, h, color)
        : Draw a bitmap data on OLED
        [Params]
            @ x : Start point of x-axis
            @ y : Start point of y-axis
            @ bitmap : A two dimensional array which consist of 0 and 1, 0 is black and 1 is white
            @ w : Width of bitmap data
            @ h : Height of bitmap data
            @ color : The color of a character. BLACK(0) or WHITE(1)
    - setCursor(x, y)
        : Set the cursor on OLED, This value is used in write()
        [Params]
            @ x : x-axis point of cursor
            @ y : y-axis point of cursor
    - setTextSize(s)
        : Set text size, This value is used in write()
        [Params]
            @ s : Pixel size of charactor strock. Default is 1
    - setTextColor(c)
        : Set text color, This value is used in write()
        [Params]
            @ c : Text color value. BLACK(0) or WHITE(1)
    - setTextColorWithBg(c, b)
        : Set text color and background color, This value is used in write()
        [Params]
            @ c : Text color value. BLACK(0) or WHITE(1)
            @ b : Background color value. BLACK(0) or WHITE(1)
    - width()
        : Retun widht of OLED
    - height()
        : Return height of OLED
    - drawPixel(x, y, color)
        : Draw a dot on OLED
        [Params]
            @ x : The point of a dot
            @ y : The point of a dot
            @ color : The color of a dot
    - setBrightness(Brightness)
        : Set brightness of OLED
        [Params]
            @ Brightness : Brightness value to be set
    - invertDisplay(i)
        : Change display mode.
        [Params]
            @ i : If i is True, dispaly mode is Inverse mode but if i is False, display mode is Normal mode. In Inverse mode, 0 is white and 1 is black.
    - startscrollright(start, stop)
        : Scroll the screen in the row-right direction, Scroll method isn't working in OLED_SH1106_I2C_128x64
        [Params]
            @ start : Start point of scrolling
            @ stop : Stop point of scrolling
    - startscrollleft(start, stop)
        : Scroll the screen in the row-left direction, Scroll method isn't working in OLED_SH1106_I2C_128x64
        [Params]
            @ start : Start point of scrolling
            @ stop : Stop point of scrolling
    - startscrolldiagright(start, stop)
        : Scroll the screen in the column-right direction, Scroll method isn't working in OLED_SH1106_I2C_128x64
        [Params]
            @ start : Start point of scrolling
            @ stop : Stop point of scrolling
    - startscrolldiagleft(start, stop)
        : Scroll the screen in the column-left direction, Scroll method isn't working in OLED_SH1106_I2C_128x64
        [Params]
            @ start : Start point of scrolling
            @ stop : Stop point of scrolling
    - stopscroll()
        : Stop scrolling the screen
    - display()
        : Display buffer data on OLED
    - clearDisplay()
        : Clear the data on OLED
    - write(c)
        : Write the character at location of cursor on OLED
        [Params]
            @ c : The character to be written

*********************************** Class Gesture **********************************

[Class Description]

    - Apds9960 Controlled via I2C Interface 
    - Apds9960()
        : Gesture object inheriting from I2C Class (I2c Slave Address -> 0x39)

[Defines]

    - APDS9960_MODE_[mode] - mode: POWER, AMBIENT_LIGHT, PROXIMITY, WAIT, AMBIENT_LIGHT_INT, PROXIMITY_INT, GESTURE, ALL
        : Flag of each modes.
    - APDS9960_DIR_[direction] - direction: NONE, LEFT, RIGHT, DOWN, NEAR, FAR, ALL
        : Definition of detedted gesture motion direction, You can compare with readGesture() return value

[Functions]

    - getMode()
        : Get mode of gesture sensor
    - setMode(mode, enable=True)
        : Set selected mode enable or disable, Call this method in all enable/disable method
        [Params]
            @ mode : The mode to be changed status(enable or disable), ex) APDS9960_MODE_POWER
            @ enable : Status of selected mode, True or False, Default is True
    - enableLightSensor(interrupts=True)
        : Enable APDS9960 as light sensor
        [Params]
            @ interrupts : Allow interrupt or not, Default is True
    - disableLightSensor()
        : Disable light sensor
    - enableProximitySensor(interrupts=True)
        : Enable APDS9960 as proximity sensor
        [Params]
            @ interrupts : Allow interrupt or not, Default is True
    - disableProximitySensor()
        : disable proximity sensor
    - enableGestureSensor(interrupts=True)
        : Enable APDS9960 as gesture sensor
        [Params]
            @ interrupts : Allow interrupt or not, Default is True
    - disableGestureSensor()
        : Disable gesture sensor
    - isGestureAvailable()
        : Return True if gesture sensor is available, else return False
    - readGesture()
        : Return gesture motion direction number
    - enablePower()
        : Enable power of APDS9960
    - disablePower()
        : Disable power of APDS9960
    - readAmbientLight()
        : Read ambient light raw data from register (2 byte data)
    - readRedLight()
        : Read red light raw data from register (2 byte data)
    - readGreenLight()
        : Read green light raw data from register (2 byte data)
    - readBlueLight()
        : Read blue light raw data from register (2 byte data)
    - readProximity()
        : Read proximity raw data from register (1 byte data)
    - resetGestureParameters()
        : Reset all parameters of gesture sensor as 0
    - processGestureData()
        : Process gesture sensor data, Return True If it finished, Else return False
    - decodeGesture()
        : Decode gesture sensor data, Return True If it finished, Else return False
    - getProxIntLowThresh()
        : Get proximity interrupt low threshold raw data from register
    - setProxIntLowThresh(threshold)
        : Set proximity interrupt low threshold register data
        [Params]
            @ threshold : Low threshold value to set register
    - getProxIntHighThresh()
        : Get proximity interrupt high threshold raw data from register
    - setProxIntHighThresh(threshold)
        : Set proximity interrupt high threshold register data
        [Params]
            @ threshold : High threshold value to set register
    - getLEDDrive()
        : Get LED Drive raw data from register, It is the intensity of the IR emission
    - setLEDDrive(drive)
        : Set LED drive register data
        [Params]
            @ drive : Drive register value to set register, Value means the intensity of the IR emission
    - getProximityGain()
        : Get proximity gain raw data from register
    - setProximityGain(drive)
        : Set proximity gain register data
        [Params]
            @ drive : Gain value to set register
    - getAmbientLightGain()
        : Get ambient light gain raw data from register
    - setAmbientLightGain(drive)
        : Set ambient light gain register data
        [Params]
            @ drive : Gain value to set register
    - getLEDBoost()
        : Get LED boost raw data from register
    - setLEDBoost(boost)
        : Set LED boost register data
        [Params]
            @ drive : LED boost value to set register
    - getProxGainCompEnable()
        : Get the proximity gain compensation is enabled
    - setProxGainCompEnable(enable)
        : Enable or disable the proximity gain compensation
        [Params]
            @ enable : If True, enable gain compensation
    - getProxPhotoMask()
        : Get the proximity photo mask
    - setProxPhotoMask(mask)
        : Set the proximity photo mask
        [Params]
            @ mask : Proximity photo mask
    - getGestureEnterThresh()
        : Get gesture enter threshold raw data from register
    - setGestureEnterThresh(threshold)
        : Set gesture enter threshold register data
        [Params]
            @ threshold : Enter threshold value to set register
    - getGestureExitThresh()
        : Get gesture exit threshold raw data from register
    - setGestureExitThresh(threshold)
        : Set gesture exit threshold register data
        [Params]
            @ threshold : Exit threshold value to set register
    - getGestureGain()
        : Get gesture gain raw data from register
    - setGestureGain(gain)
        : Set gesture gain register data
        [Params]
            @ drive : Gesture gain value to set register
    - getGestureLEDDrive()
        : Set gesture LED Drive raw data from register
    - setGestureLEDDrive(drive)
        : Set gesture LED drive register data
        [Params]
            @ drive : Gesture LED drive value to set register
    - getGestureWaitTime()
        : Get gesture wait time raw data from register
    - setGestureWaitTime(time)
        : Set gesture wait time register data
        [Params]
            @ time : Gesture wait time value to set register
    - getLightIntLowThreshold()
        : Get light interrupt low threshold raw data from register
    - setLightIntLowThreshold(threshold)
        : Set light interrupt low threshold register data
        [Params]
            @ threshold : Light interrupt low threshold value to set register
    - getLightIntHighThreshold()
        : Get light interrupt high threshold raw data from register
    - setLightIntHighThreshold(threshold)
        : Set light interrupt high threshold register data
        [Params]
            @ threshold : Light interrupt low threshold value to set register
    - getProximityIntLowThreshold()
        : Same with getProxIntLowThresh()
    - setProximityIntLowThreshold(threshold)
        : Same with setProxIntLowThresh(threshold)
    - getProximityIntHighThreshold()
        : Same with getProxIntHighThresh()
    - setProximityIntHighThreshold(threshold)
        : Same with setProxIntHightThresh(threshold)
    - getAmbientLightIntEnable()
        : Get ambient light interrupt is enabled
    - setAmbientLightIntEnable(enable)
        : Enable or disable ambient light interrupt
        [Params]
            @ enable : If true, enable ambient light interrupt
    - getProximityIntEnable()
        : Get proximity interrupt is enabled
    - setProximityIntEnable(enable)
        : Enable or disable proximity interrupt
        [Params]
            @ enable : If true, enable proximity interrupt
    - getGestureIntEnable()
        : Get gesture interrupt is enabled
    - setGestureIntEnable(enable)
        : Enable or disable gesture interrupt
        [Params]
            @ enable : If true, enable gesture interrupt
    - clearAmbientLightInt()
        : Disable ambient light interrupt
    - clearProximityInt()
        : Disable proximity interrupt
    - getGestureMode()
        : Get gesture mode is enabled
    - setGestureMode(enable)
        : Enable or disalbe gesture mode
        [Params]
            @ enable : If true, enable gesture mode