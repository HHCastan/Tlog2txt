package com.flamingo.util;

import java.io.PrintWriter;
import java.io.FileInputStream;
import java.io.IOException;

public class HexDump {
	public static void hexDump(String out, FileInputStream in) throws IOException {
		int c = 0;
		String st;

		PrintWriter writer = new PrintWriter(out, "UTF-8");

		while ((c = in.read()) != -1) {
			st = String.format("%02x", c & 0xff);

			switch (c) {
			case 13: // carriage return (0D)
				c = in.read();
				if (c == 10) { // NL line feed (0A)
					writer.print("\n ============================================= \n");
					c = in.read();
				}
				break;
			case 0:
				writer.print("00");
				break;
			case 58: // (:)
				writer.print(":");
				break;
			case 34: // (22 -> ")
				c = in.read();
				if (c == 44) { // comma (2c -> ,)
					c = in.read();
					if (c == 34) { // (22 -> ")
						writer.print("\n - - - - \n");
					} else {
						in.skip(-1);
					}
				} else {
					if (c == 13) {  // carriage return (0D)
						in.skip(-1);
						break;
					}
					writer.print("22");
					in.skip(-1);
				}
				break;
			default:
				writer.print(st);
			}

		}
		in.close();
		writer.close();
	}

	public static void main(String[] args) throws IOException, Exception {
		hexDump("s:/tmp/out.txt", new FileInputStream("s:/tmp/eamtranb.dat"));
	}

}
