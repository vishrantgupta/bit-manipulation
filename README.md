## Bit manipulation functions

```
/** Returns Character array
  *
  * @return Array[Char]
  */
def getChars(bytes: Array[Byte]): Array[Char] = {
  bytes.map(b => b.toChar)
}

/** Returns Boolean value from byte
  *
  * @return Boolean
  */
def bytesToDbool(bytes: Array[Byte]): Boolean = bytes(0) != 0

/** Wraps array of bytes to ByteBuffer
  *
  * @return ByteBuffer
  */
def wrapByteBuffer(bytes: Array[Byte]): ByteBuffer = ByteBuffer.wrap(bytes)

/** Returns `Double` representation from Byte array
  *
  * @return Double
  */
def bytesToDouble(bytes: Array[Byte]): Double = wrapByteBuffer(bytes).getDouble

/** Returns `Float` representation from Byte array
  *
  * @return Float
  */
def bytesToFloat(bytes: Array[Byte]): Float = wrapByteBuffer(bytes).getFloat

/** Returns signed `Int` representation from Byte array
  *
  * @return Int
  */
def bytesToSignedInt(bytes: Array[Byte], size: Int): Int = {
  new BigInteger(bytes).intValue() << 32 - size >> 32 - size
}

/** Returns unsigned `Int` representation from Byte array of size 1 or 2 i.e., uint8_t and uint16_t
  *
  * @return Int
  */
def bytesToUint(b: Array[Byte]): Int = {
  val l = 0

  // iterate
  // first left shit l
  // l = l | b(0) & 0xFF

  b.foldLeft(l) { (x, byte) =>
    val y = x << 8
    val z = y | byte & 0xFF
    z
  }
}

/** Returns unsigned `Int` representation from Byte array of size 4 i.e., uint32_t
  *
  * @return Long
  */
def bytesToUint32(b: Array[Byte]): Long = { //  uint32_t

  val l = 0L
  b.foldLeft(l) { (x, byte) =>
    val y = x << 8
    val z = y | byte & 0xFF
    z
  }
}

/** Returns unsigned `Int` array representation from Byte array for uint8_t
  *
  * @return Array[Int]
  */
def bytesToUint8Array(byteArray: Array[Byte]): Array[Int] = {

  val ints = new Array[Int](byteArray.length)

  ints.zipWithIndex.map(v => 0x00 << 24 | byteArray(v._2) & 0xff)
}

/** Returns array of `Double` from Byte array
  *
  * @return Array[Double]
  */
def bytesToDoubleArray(byteArray: Array[Byte]): Array[Double] = {

  val times = 64 / 8
  val doubles = new Array[Double](byteArray.length / times)

  doubles.zipWithIndex.map(i => ByteBuffer.wrap(byteArray, i._2 * times, times).getDouble)
}

/** Returns array of `Float` from Byte array
  *
  * @return Array[Float]
  */
def bytesToFloatArray(byteArray: Array[Byte]): Array[Float] = {

  val times = 32 / 8
  val floats = new Array[Float](byteArray.length / times)

  floats.zipWithIndex.map(i => ByteBuffer.wrap(byteArray, i._2 * times, times).getFloat)

}
```
