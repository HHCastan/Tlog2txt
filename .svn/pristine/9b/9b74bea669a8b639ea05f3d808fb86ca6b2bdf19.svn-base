package com.flamingo.gui;

import java.awt.Desktop;
import java.awt.EventQueue;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JTextField;
import javax.swing.JButton;
import javax.swing.JLabel;
import javax.swing.JOptionPane;

import com.flamingo.util.HexDump;

public class ChoosingWindow {
	private JFrame frame;
	private JTextField txtPathIn;
	private JTextField txtPathOut;
	JFileChooser fileChooserIn = new JFileChooser();
	JFileChooser fileChooserOut = new JFileChooser();
	JLabel lblMessage = new JLabel();

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					ChoosingWindow window = new ChoosingWindow();
					window.frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the application.
	 */
	public ChoosingWindow() {
		initialize();
	}

	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 600, 280);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setTitle("Exportar TLOG");
		frame.getContentPane().setLayout(null);

		JLabel lblIn = new JLabel("TLOG File:");
		lblIn.setBounds(10, 20, 65, 20);
		txtPathIn = new JTextField();
		txtPathIn.setBounds(80, 20, 390, 23);
		frame.getContentPane().add(lblIn);
		frame.getContentPane().add(txtPathIn);
		txtPathIn.setColumns(10);

		JButton btnBrowseIn = new JButton("Explorar...");
		btnBrowseIn.setBounds(475, 20, 95, 23);
		frame.getContentPane().add(btnBrowseIn);

		JLabel lblOut = new JLabel("TXT File:");
		lblOut.setBounds(10, 70, 65, 20);
		txtPathOut = new JTextField();
		txtPathOut.setBounds(80, 70, 390, 23);
		frame.getContentPane().add(lblOut);
		frame.getContentPane().add(txtPathOut);
		txtPathOut.setColumns(10);

		JButton btnBrowseOut = new JButton("Explorar...");
		btnBrowseOut.setBounds(475, 70, 95, 23);
		frame.getContentPane().add(btnBrowseOut);
		
		JButton btnExport = new JButton("Exportar");
		btnExport.setBounds(140, 150, 120, 30);
		frame.getContentPane().add(btnExport);

		JButton btnCancel = new JButton("Cancelar");
		btnCancel.setBounds(350, 150, 120, 30);
		frame.getContentPane().add(btnCancel);

		lblMessage.setText("Seleccione TLOG a exportar");
		lblMessage.setHorizontalAlignment(0);
		lblMessage.setBounds(100, 215, 400, 20);
		frame.getContentPane().add(lblMessage);
		
		JLabel lblBy = new JLabel("by HHC");
		lblBy.setBounds(540, 222, 60, 20);
		frame.getContentPane().add(lblBy);

		btnBrowseIn.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {

				fileChooserIn.setFileSelectionMode(JFileChooser.FILES_ONLY);

				fileChooserIn.setAcceptAllFileFilterUsed(false);

				int rVal = fileChooserIn.showOpenDialog(null);
				if (rVal == JFileChooser.APPROVE_OPTION) {
					txtPathIn.setText(fileChooserIn.getSelectedFile().toString());
					//txtPathOut.setText(fileChooserIn.getSelectedFile().toString());
					String txtAux = fileChooserIn.getSelectedFile().toString();
					txtAux = txtAux.substring(0,txtAux.length()-3);
					txtAux = txtAux.concat("TXT");
					System.out.println(txtAux);
					txtPathOut.setText(txtAux);

				}
			}
		});

		btnBrowseOut.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {

				fileChooserOut.setFileSelectionMode(JFileChooser.FILES_ONLY);

				fileChooserOut.setAcceptAllFileFilterUsed(false);

				int rVal = fileChooserOut.showOpenDialog(null);
				if (rVal == JFileChooser.APPROVE_OPTION) {
					txtPathOut.setText(fileChooserOut.getSelectedFile().toString());
				}
			}
		});

		btnCancel.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {

				frame.dispose();
				System.exit(0);

			}
		});

		btnExport.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				
				String stFileIn = txtPathIn.getText();
				String stFileOut = txtPathOut.getText();
				File fFileText = new File(stFileOut);
				
				if (stFileIn.compareTo(stFileOut) == 0) {
					JOptionPane.showMessageDialog(frame, "Archivo destino debe ser diferente al origen.", "Error", JOptionPane.WARNING_MESSAGE);
					
				} else {
					
					try {
						lblMessage.setText("Exportando TLOG...");
						lblMessage.paintImmediately(lblMessage.getVisibleRect());
						HexDump.hexDump (stFileOut, new FileInputStream(stFileIn));
						Desktop.getDesktop().open(fFileText);
					} catch (FileNotFoundException e1) {
						JOptionPane.showMessageDialog(frame, "Archivo seleccionado no existe.", "Error", JOptionPane.WARNING_MESSAGE);
					} catch (IOException e1) {
						JOptionPane.showMessageDialog(frame, "Error. Revise los datos.", "Error", JOptionPane.WARNING_MESSAGE);
					}
					lblMessage.setText("Seleccione TLOG a exportar");
					lblMessage.paintImmediately(lblMessage.getVisibleRect());
				}


			}
		});

	}

}
