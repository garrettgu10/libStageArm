![# libStageARM](https://raw.githubusercontent.com/Thinkatron/libStageArm/master/Resources/libStageArmAlt.png "libStageARM Logo")

# 这是什么？
 *__libStageARM__* 是一个用C语言编绘的库，用于和位于南方卫理公会大学（SMU）的三维机械手臂沟通。它通过一个串行接口与 Arduino 沟通。这个项目的目标是提供一个易定制，易实现的界面，包含许多简单、易用、多语言的函数。它也提供一个使用任何语言都容易编绘的串行标准。它也提供一个简单的 REST 界面，用于通过网络控制机械手臂。

# What is it?
  *__libStageARM__* is a C library written to interact with the SMU 3D Stage Arm with using a simple standard serial interface. The goal of this project is to provide an easily customizable, easily implemented interface, with simple-to-use functions available in multiple languages, and a clearly defined serial interface that can be implemented an any other language. This project also provides a simple REST API for web control of the 3D Stage.

# Compatibility
|Language        |Implementation          |Tested|Succesful|
|:--------------:|------------------------|:----:|---------|
|C               |Header and Shared Object|✓     |Success  |
|C++             |Header and Shared Object|✓     |Success  |
|JavaScript      |SWIG Wrapper            |✓     |Success  |
|Java            |SWIG Wrapper            |✓     |Success  |
|Scala           |Java SWIG Wrapper       |✓     |Success  |
|Allegro CL      |SWIG Wrapper            |✗     |Unknown  |
|C#              |SWIG Wrapper            |✗     |Unknown  |
|CFFI            |SWIG Wrapper            |✗     |Unknown  |
|CLISP           |SWIG Wrapper            |✗     |Unknown  |
|Chicken         |SWIG Wrapper            |✗     |Unknown  |
|D               |SWIG Wrapper            |✗     |Unknown  |
|Go              |SWIG Wrapper            |✗     |Unknown  |
|Guile           |SWIG Wrapper            |✗     |Unknown  |
|Lua             |SWIG Wrapper            |✗     |Unknown  |
|Modula-3        |SWIG Wrapper            |✗     |Unknown  |
|Mzscheme        |SWIG Wrapper            |✗     |Unknown  |
|OCAML           |SWIG Wrapper            |✗     |Unknown  |
|Octave          |SWIG Wrapper            |✗     |Unknown  |
|Perl            |SWIG Wrapper            |✗     |Unknown  |
|PHP             |SWIG Wrapper            |✗     |Unknown  |
|Python          |SWIG Wrapper            |✗     |Unknown  |
|R               |SWIG Wrapper            |✗     |Unknown  |
|Ruby            |SWIG Wrapper            |✗     |Unknown  |
|Scilab          |SWIG Wrapper            |✗     |Unknown  |
|Tcl             |SWIG Wrapper            |✗     |Unknown  |
|UFFI            |SWIG Wrapper            |✗     |Unknown  |
>If you test a language, please make a pull request.
>If you create a wrapper or implementation in an unlisted language,
>please, feel free to make a pull request with an update to the
>table and your implementation.
>
>Thank you!
# Serial Standard
 Any control command for the 3D Platform will be a single Byte (unsigned char / uChar / uInt_8) along, followed by a command-specific buffer array. All commands are little-endian. The Buffer Size includes the Initial Byte and the Arguments. Every action will respind with 0 for a successful action or a non-zero value for an unsuccessful action. Some actions will have specific responses for certian errors, but will usually just return 1 if they are unsuccessful.
 
 ### Commands
 
|Command          |Initial Byte |Buffer Size |Arguments |
|-----------------|:-----------:|:----------:|----------|
|Begin New Set    |0x00         |1           |None      |

### Error Codes

|Error Code |Meaning                                                              |
|:---------:|---------------------------------------------------------------------|
|0x00       |Success                                                              |
|0x01       |Generic Failure                                                      |
|0x02       |Coordinate out of bounds, no action                                  |
|0x03       |Coordinate out of bounds, reached outer bound X                      |
|0x04       |Coordinate out of bounds, reached outer bound Y                      |
|0x05       |Coordinate out of bounds, reached outer bound Z                      |
|0x06       |Coordinate out of bounds, reached outer bound X & Y                  |
|0x07       |Coordinate out of bounds, reached outer bound Y & Z                  |
|0x08       |Coordinate out of bounds, reached outer bound Z & X                  |
|0x09       |Coordinate out of bounds, reached outer bound X & Y & Z              |
|0x0A       |Coordinate out of bounds, undefined action (Recallibration Suggested)|


# REST API

Send command as string in get request. Delimit args with "~" Returns a JSON object formatted like so:
```javascript
{
   "Success:" : true|false;
   "Error"    : "Error String"|null
}
```

|Request |Command |Args     |
|--------|--------|---------|
|Move    |Move    |"X\~Y\~Z"|
