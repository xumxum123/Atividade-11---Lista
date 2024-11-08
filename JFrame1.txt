package lista.view;

import java.awt.EventQueue;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import lista.model.Aluno;
import javax.swing.JTextField;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.util.ArrayList;

public class JFrame1 extends JFrame {

    private static final long serialVersionUID = 1L;
    private JPanel contentPane;
    private JTextField txt_nome;
    private JTextField txt_telefone;
    private static ArrayList<Aluno> listaAlunos = new ArrayList<>();

    public static void main(String[] args) {
        EventQueue.invokeLater(new Runnable() {
            public void run() {
                try {
                    JFrame1 frame = new JFrame1();
                    frame.setVisible(true);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
    }

    public JFrame1() {
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setBounds(100, 100, 450, 300);
        contentPane = new JPanel();
        contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));

        setContentPane(contentPane);
        contentPane.setLayout(null);
        
        txt_nome = new JTextField();
        txt_nome.setToolTipText("Nome do Aluno");
        txt_nome.setBounds(49, 40, 245, 19);
        contentPane.add(txt_nome);
        txt_nome.setColumns(10);
        
        txt_telefone = new JTextField();
        txt_telefone.setToolTipText("Telefone do Aluno");
        txt_telefone.setBounds(49, 90, 245, 19);
        contentPane.add(txt_telefone);
        txt_telefone.setColumns(10);
        
        JButton btn_Cadastrar = new JButton("Cadastrar");
        btn_Cadastrar.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String nome = txt_nome.getText();
                String telefone = txt_telefone.getText();
                if(!nome.isEmpty() && !telefone.isEmpty()) {
                    Aluno aluno = new Aluno(nome, telefone);
                    listaAlunos.add(aluno);
                    JOptionPane.showMessageDialog(btn_Cadastrar, "Cadastrado Com Sucesso");
                    txt_nome.setText("");
                    txt_telefone.setText("");
                } else {
                    JOptionPane.showMessageDialog(btn_Cadastrar, "Campos Vazios");
                }
            }
        });
        btn_Cadastrar.setBounds(49, 140, 245, 25);
        contentPane.add(btn_Cadastrar);
        
        JButton btn_Listar = new JButton("Listar");
        btn_Listar.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                JFrame2 jFrame2 = new JFrame2(listaAlunos);
                jFrame2.setVisible(true);
            }
        });
        btn_Listar.setBounds(236, 222, 117, 25);
        contentPane.add(btn_Listar);
    }
}
