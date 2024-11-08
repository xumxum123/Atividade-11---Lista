package lista.view;

import java.awt.EventQueue;
import java.util.ArrayList;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import lista.model.Aluno;
import javax.swing.JComboBox;
import javax.swing.JLabel;
import javax.swing.JTextField;
import javax.swing.JButton;
import javax.swing.JOptionPane;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class JFrame2 extends JFrame {

    private static final long serialVersionUID = 1L;
    private JPanel contentPane;
    private JTextField txt_nome;
    private JTextField txt_telefone;
    
    public JFrame2(ArrayList<Aluno> listaAlunos) {
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setBounds(100, 100, 450, 300);
        contentPane = new JPanel();
        contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));

        setContentPane(contentPane);
        contentPane.setLayout(null);

        JLabel lbl_nome = new JLabel("Nome");
        lbl_nome.setBounds(148, 78, 70, 15);
        contentPane.add(lbl_nome);

        JLabel lbl_telefone = new JLabel("Telefone");
        lbl_telefone.setBounds(148, 120, 70, 15);
        contentPane.add(lbl_telefone);

        txt_nome = new JTextField();
        txt_nome.setBounds(230, 75, 150, 20);
        contentPane.add(txt_nome);
        txt_nome.setColumns(10);
        txt_nome.setEditable(false);
        
        txt_telefone = new JTextField();
        txt_telefone.setBounds(230, 117, 150, 20);
        contentPane.add(txt_telefone);
        txt_telefone.setColumns(10);
        txt_telefone.setEditable(false);

        JComboBox<Aluno> comboBox = new JComboBox<>(listaAlunos.toArray(new Aluno[0]));
        comboBox.setBounds(80, 20, 207, 24);
        contentPane.add(comboBox);

        comboBox.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                Aluno alunoSelecionado = (Aluno) comboBox.getSelectedItem();
                if (alunoSelecionado != null) {
                    txt_nome.setText(alunoSelecionado.getNome());
                    txt_telefone.setText(alunoSelecionado.getTelefone());
                    txt_nome.setEditable(true);
                    txt_telefone.setEditable(true);
                }
            }
        });

        JButton btn_Atualizar = new JButton("Atualizar");
        btn_Atualizar.setBounds(80, 170, 100, 25);
        contentPane.add(btn_Atualizar);
        btn_Atualizar.setEnabled(false);

        btn_Atualizar.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                Aluno alunoSelecionado = (Aluno) comboBox.getSelectedItem();
                if (alunoSelecionado != null) {
                    alunoSelecionado.setNome(txt_nome.getText());
                    alunoSelecionado.setTelefone(txt_telefone.getText());
                    JOptionPane.showMessageDialog(btn_Atualizar, "Aluno atualizado com sucesso");
                    txt_nome.setText("");
                    txt_telefone.setText("");
                    txt_nome.setEditable(false);
                    txt_telefone.setEditable(false);
                    comboBox.setModel(new JComboBox<>(listaAlunos.toArray(new Aluno[0])).getModel());
                }
            }
        });

        JButton btn_Excluir = new JButton("Excluir");
        btn_Excluir.setBounds(230, 170, 100, 25);
        contentPane.add(btn_Excluir);

        btn_Excluir.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int response = JOptionPane.showConfirmDialog(null, "Tem certeza que deseja excluir?", "Confirmação", JOptionPane.YES_NO_OPTION);
                if (response == JOptionPane.YES_OPTION) {
                    Aluno alunoSelecionado = (Aluno) comboBox.getSelectedItem();
                    if (alunoSelecionado != null) {
                        listaAlunos.remove(alunoSelecionado);
                        JOptionPane.showMessageDialog(btn_Excluir, "Aluno excluído com sucesso");
                        txt_nome.setText("");
                        txt_telefone.setText("");
                        txt_nome.setEditable(false);
                        txt_telefone.setEditable(false);
                        comboBox.setModel(new JComboBox<>(listaAlunos.toArray(new Aluno[0])).getModel());
                    }
                }
            }
        });

        comboBox.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                Aluno alunoSelecionado = (Aluno) comboBox.getSelectedItem();
                if (alunoSelecionado != null) {
                    txt_nome.setText(alunoSelecionado.getNome());
                    txt_telefone.setText(alunoSelecionado.getTelefone());
                    txt_nome.setEditable(true);
                    txt_telefone.setEditable(true);
                    btn_Atualizar.setEnabled(true);
                }
            }
        });
    }
}
