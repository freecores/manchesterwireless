Usage: 

Open globals.vhd. Change WORD_LENGTH to the number of bits to be received -- this is the number of bits _before_ Manchester encoding. 

The constants: INTERVAL_MAX_DOUBLE, INTERVAL_MIN_DOUBLE, INTERVAL_MAX_SINGLE, INTERVAL_MIN_SINGLE, INTERVAL_QUADRUPLE set the window of FPGA clocks needed to classify a single/double one/zero. For example, if transmission arrives at 1K BAUD, then each bit is 1ms long. If the FPGA clock is 50MHz, giving a period of 2E-8, then 50K FPGA clocks will occur each bit. Therefore set INTERVAL_MIN/MAX_SINGLE to be somewhere on either end of 50K, for example 10K and 75K. Do similar for INTERVAL_MIN/MAX_DOUBLE. Unfortunately, you will probably need to experiment to see how static your transmitter BAUD really is.

Out of the box, the decodeManchester core will decode one transmission, then stop, waiting to be reset, until the next signal is decodable. See synthTest.vhd for a simple way to reset the circuit after each received bit.

TODO:

When testing this circuit with an ASK transmitter/receiver pair, random radio noise was a huge problem. There needs to be a way to strengthen the protocol. Also, I believe, it is from the quality of the ASK equipment, the twoToOne subcore misses some bits, causing frustrating noise to be permitted into the system.