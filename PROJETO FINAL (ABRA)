import java.util.*;
import java.util.stream.Collectors;
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.awt.event.*;

enum StatusTarefa {
    PENDENTE, EM_PROGRESSO, CONCLUIDA;
}

class Categoria {
    private static int contador = 1;
    private int id;
    private String nome;

    public Categoria(String nome) {
        this.id = contador++;
        this.nome = nome;
    }
    public int getId() { return id; }
    public String getNome() { return nome; }
    public void setNome(String nome) { this.nome = nome; }
    @Override
    public String toString() { return nome; }
}

class Colaborador {
    private static int contador = 1;
    private int id;
    private String nome;

    public Colaborador(String nome) {
        this.id = contador++;
        this.nome = nome;
    }
    public int getId() { return id; }
    public String getNome() { return nome; }
    public void setNome(String nome) { this.nome = nome; }
    @Override
    public String toString() { return nome; }
}

class Tarefa {
    private static int contador = 1;
    private int id;
    private String titulo;
    private String descricao;
    private StatusTarefa status;
    private Categoria categoria;
    private Colaborador colaborador;

    public Tarefa(String titulo, String descricao, Categoria categoria) {
        this.id = contador++;
        this.titulo = titulo;
        this.descricao = descricao;
        this.status = StatusTarefa.PENDENTE;
        this.categoria = categoria;
        this.colaborador = null;
    }
    public int getId() { return id; }
    public String getTitulo() { return titulo; }
    public void setTitulo(String titulo) { this.titulo = titulo; }
    public String getDescricao() { return descricao; }
    public void setDescricao(String descricao) { this.descricao = descricao; }
    public StatusTarefa getStatus() { return status; }
    public void setStatus(StatusTarefa status) { this.status = status; }
    public Categoria getCategoria() { return categoria; }
    public void setCategoria(Categoria categoria) { this.categoria = categoria; }
    public Colaborador getColaborador() { return colaborador; }
    public void setColaborador(Colaborador colaborador) { this.colaborador = colaborador; }
    @Override
    public String toString() {
        return String.format("%d - %s [%s]", id, titulo, status);
    }
}

class SistemaControleTarefas {
    private Map<Integer, Categoria> categorias = new HashMap<>();
    private Map<Integer, Colaborador> colaboradores = new HashMap<>();
    private Map<Integer, Tarefa> tarefas = new HashMap<>();

    public Categoria criarCategoria(String nome) {
        Categoria c = new Categoria(nome);
        categorias.put(c.getId(), c);
        return c;
    }
    public Categoria lerCategoria(int id) {
        if (!categorias.containsKey(id))
            throw new NoSuchElementException("Categoria não encontrada!");
        return categorias.get(id);
    }
    public void atualizarCategoria(int id, String novoNome) {
        Categoria c = lerCategoria(id);
        c.setNome(novoNome);
    }
    public void deletarCategoria(int id) {
        if (!categorias.containsKey(id))
            throw new NoSuchElementException("Categoria não encontrada!");
        categorias.remove(id);
        tarefas.values().forEach(t -> {
            if (t.getCategoria() != null && t.getCategoria().getId() == id) {
                t.setCategoria(null);
            }
        });
    }
    public List<Categoria> listarCategorias() {
        return new ArrayList<>(categorias.values());
    }

    public Colaborador criarColaborador(String nome) {
        Colaborador c = new Colaborador(nome);
        colaboradores.put(c.getId(), c);
        return c;
    }
    public Colaborador lerColaborador(int id) {
        if (!colaboradores.containsKey(id))
            throw new NoSuchElementException("Colaborador não encontrado!");
        return colaboradores.get(id);
    }
    public void atualizarColaborador(int id, String novoNome) {
        Colaborador c = lerColaborador(id);
        c.setNome(novoNome);
    }
    public void deletarColaborador(int id) {
        if (!colaboradores.containsKey(id))
            throw new NoSuchElementException("Colaborador não encontrado!");
        colaboradores.remove(id);
        tarefas.values().forEach(t -> {
            if (t.getColaborador() != null && t.getColaborador().getId() == id) {
                t.setColaborador(null);
            }
        });
    }
    public List<Colaborador> listarColaboradores() {
        return new ArrayList<>(colaboradores.values());
    }

    public Tarefa criarTarefa(String titulo, String descricao, int categoriaId) {
        Categoria c = lerCategoria(categoriaId);
        Tarefa t = new Tarefa(titulo, descricao, c);
        tarefas.put(t.getId(), t);
        return t;
    }
    public Tarefa lerTarefa(int id) {
        if (!tarefas.containsKey(id))
            throw new NoSuchElementException("Tarefa não encontrada!");
        return tarefas.get(id);
    }
    public void atualizarTarefa(int id, String novoTitulo, String novaDescricao, int categoriaId) {
        Tarefa t = lerTarefa(id);
        Categoria c = lerCategoria(categoriaId);
        t.setTitulo(novoTitulo);
        t.setDescricao(novaDescricao);
        t.setCategoria(c);
    }
    public void deletarTarefa(int id) {
        if (!tarefas.containsKey(id))
            throw new NoSuchElementException("Tarefa não encontrada!");
        tarefas.remove(id);
    }

    public void associarTarefaColaborador(int tarefaId, int colaboradorId) {
        Tarefa t = lerTarefa(tarefaId);
        Colaborador c = lerColaborador(colaboradorId);
        t.setColaborador(c);
    }

    public void alterarStatusTarefa(int tarefaId, StatusTarefa novoStatus) {
        Tarefa t = lerTarefa(tarefaId);
        t.setStatus(novoStatus);
    }

    public List<Tarefa> listarTarefas(Integer colaboradorId, Integer categoriaId, StatusTarefa status) {
        return tarefas.values().stream()
            .filter(t -> (colaboradorId == null || (t.getColaborador() != null && t.getColaborador().getId() == colaboradorId)))
            .filter(t -> (categoriaId == null || (t.getCategoria() != null && t.getCategoria().getId() == categoriaId)))
            .filter(t -> (status == null || t.getStatus() == status))
            .collect(Collectors.toList());
    }

    public List<Tarefa> listarTodasTarefas() {
        return new ArrayList<>(tarefas.values());
    }
}

public class SistemaControleTarefasGUI extends JFrame {
    private SistemaControleTarefas sistema;
    private DefaultListModel<Categoria> modelCategorias = new DefaultListModel<>();
    private JList<Categoria> listCategorias = new JList<>(modelCategorias);
    private DefaultListModel<Colaborador> modelColaboradores = new DefaultListModel<>();
    private JList<Colaborador> listColaboradores = new JList<>(modelColaboradores);
    private DefaultTableModel modelTarefas;
    private JTable tableTarefas;

    public SistemaControleTarefasGUI() {
        sistema = new SistemaControleTarefas();
        setTitle("Sistema de Controle de Tarefas");
        setSize(800, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        JTabbedPane tabs = new JTabbedPane();
        tabs.addTab("Categorias", criarPainelCategorias());
        tabs.addTab("Colaboradores", criarPainelColaboradores());
        tabs.addTab("Tarefas", criarPainelTarefas());
        add(tabs);
        atualizarCategorias();
        atualizarColaboradores();
        atualizarTarefas(null, null, null);
    }

    private JPanel criarPainelCategorias() {
        JPanel panel = new JPanel(new BorderLayout());
        JScrollPane scroll = new JScrollPane(listCategorias);
        panel.add(scroll, BorderLayout.CENTER);
        JPanel painelBotoes = new JPanel();

        JButton btnAdd = new JButton("Adicionar");
        btnAdd.addActionListener(e -> {
            String nome = JOptionPane.showInputDialog(this, "Nome da categoria:");
            if (nome != null && !nome.trim().isEmpty()) {
                try {
                    sistema.criarCategoria(nome.trim());
                    atualizarCategorias();
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnAdd);

        JButton btnEditar = new JButton("Editar");
        btnEditar.addActionListener(e -> {
            Categoria selecionada = listCategorias.getSelectedValue();
            if (selecionada == null) {
                JOptionPane.showMessageDialog(this, "Selecione uma categoria para editar.");
                return;
            }
            String novoNome = JOptionPane.showInputDialog(this, "Novo nome:", selecionada.getNome());
            if (novoNome != null && !novoNome.trim().isEmpty()) {
                try {
                    sistema.atualizarCategoria(selecionada.getId(), novoNome.trim());
                    atualizarCategorias();
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnEditar);

        JButton btnExcluir = new JButton("Excluir");
        btnExcluir.addActionListener(e -> {
            Categoria selecionada = listCategorias.getSelectedValue();
            if (selecionada == null) {
                JOptionPane.showMessageDialog(this, "Selecione uma categoria para excluir.");
                return;
            }
            int confirm = JOptionPane.showConfirmDialog(this, "Excluir categoria " + selecionada.getNome() + "?");
            if (confirm == JOptionPane.YES_OPTION) {
                try {
                    sistema.deletarCategoria(selecionada.getId());
                    atualizarCategorias();
                    atualizarTarefas(null,null,null);
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnExcluir);

        panel.add(painelBotoes, BorderLayout.SOUTH);
        return panel;
    }

    private JPanel criarPainelColaboradores() {
        JPanel panel = new JPanel(new BorderLayout());
        JScrollPane scroll = new JScrollPane(listColaboradores);
        panel.add(scroll, BorderLayout.CENTER);
        JPanel painelBotoes = new JPanel();

        JButton btnAdd = new JButton("Adicionar");
        btnAdd.addActionListener(e -> {
            String nome = JOptionPane.showInputDialog(this, "Nome do colaborador:");
            if (nome != null && !nome.trim().isEmpty()) {
                try {
                    sistema.criarColaborador(nome.trim());
                    atualizarColaboradores();
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnAdd);

        JButton btnEditar = new JButton("Editar");
        btnEditar.addActionListener(e -> {
            Colaborador selecionado = listColaboradores.getSelectedValue();
            if (selecionado == null) {
                JOptionPane.showMessageDialog(this, "Selecione um colaborador para editar.");
                return;
            }
            String novoNome = JOptionPane.showInputDialog(this, "Novo nome:", selecionado.getNome());
            if (novoNome != null && !novoNome.trim().isEmpty()) {
                try {
                    sistema.atualizarColaborador(selecionado.getId(), novoNome.trim());
                    atualizarColaboradores();
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnEditar);

        JButton btnExcluir = new JButton("Excluir");
        btnExcluir.addActionListener(e -> {
            Colaborador selecionado = listColaboradores.getSelectedValue();
            if (selecionado == null) {
                JOptionPane.showMessageDialog(this, "Selecione um colaborador para excluir.");
                return;
            }
            int confirm = JOptionPane.showConfirmDialog(this, "Excluir colaborador " + selecionado.getNome() + "?");
            if (confirm == JOptionPane.YES_OPTION) {
                try {
                    sistema.deletarColaborador(selecionado.getId());
                    atualizarColaboradores();
                    atualizarTarefas(null,null,null);
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnExcluir);

        panel.add(painelBotoes, BorderLayout.SOUTH);
        return panel;
    }

    private JPanel criarPainelTarefas() {
        JPanel panel = new JPanel(new BorderLayout());
        modelTarefas = new DefaultTableModel(new Object[]{"ID", "Título", "Descrição", "Status", "Categoria", "Colaborador"}, 0);
        tableTarefas = new JTable(modelTarefas);
        JScrollPane scroll = new JScrollPane(tableTarefas);
        panel.add(scroll, BorderLayout.CENTER);
        JPanel painelBotoes = new JPanel();

        JButton btnAdd = new JButton("Adicionar");
        btnAdd.addActionListener(e -> abrirDialogTarefa(null));
        painelBotoes.add(btnAdd);

        JButton btnEditar = new JButton("Editar");
        btnEditar.addActionListener(e -> {
            int linha = tableTarefas.getSelectedRow();
            if (linha < 0) {
                JOptionPane.showMessageDialog(this, "Selecione uma tarefa para editar.");
                return;
            }
            int tarefaId = (int) modelTarefas.getValueAt(linha, 0);
            Tarefa t = sistema.lerTarefa(tarefaId);
            abrirDialogTarefa(t);
        });
        painelBotoes.add(btnEditar);

        JButton btnExcluir = new JButton("Excluir");
        btnExcluir.addActionListener(e -> {
            int linha = tableTarefas.getSelectedRow();
            if (linha < 0) {
                JOptionPane.showMessageDialog(this, "Selecione uma tarefa para excluir.");
                return;
            }
            int tarefaId = (int) modelTarefas.getValueAt(linha, 0);
            int confirm = JOptionPane.showConfirmDialog(this, "Excluir tarefa?");
            if (confirm == JOptionPane.YES_OPTION) {
                try {
                    sistema.deletarTarefa(tarefaId);
                    atualizarTarefas(null,null,null);
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(this, "Erro: " + ex.getMessage());
                }
            }
        });
        painelBotoes.add(btnExcluir);

        JButton btnAlterarStatus = new JButton("Alterar Status");
        btnAlterarStatus.addActionListener(e -> {
            int linha = tableTarefas.getSelectedRow();
            if (linha < 0) {
                JOptionPane.showMessageDialog(this, "Selecione uma tarefa para alterar status.");
                return;
            }
            int tarefaId = (int) modelTarefas.getValueAt(linha, 0);
            Tarefa t = sistema.lerTarefa(tarefaId);
            StatusTarefa novoStatus = (StatusTarefa) JOptionPane.showInputDialog(
                this, "Selecione novo status:",
                "Alterar Status",
                JOptionPane.QUESTION_MESSAGE,
                null,
                StatusTarefa.values(),
                t.getStatus()
            );
            if (novoStatus != null) {
                sistema.alterarStatusTarefa(tarefaId, novoStatus);
                atualizarTarefas(null,null,null);
            }
        });
        painelBotoes.add(btnAlterarStatus);

        JButton btnAssociarColaborador = new JButton("Associar Colaborador");
        btnAssociarColaborador.addActionListener(e -> {
            int linha = tableTarefas.getSelectedRow();
            if (linha < 0) {
                JOptionPane.showMessageDialog(this, "Selecione uma tarefa para associar colaborador.");
                return;
            }
            int tarefaId = (int) modelTarefas.getValueAt(linha, 0);
            Tarefa t = sistema.lerTarefa(tarefaId);
            List<Colaborador> colaboradores = sistema.listarColaboradores();
            if (colaboradores.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Nenhum colaborador cadastrado.");
                return;
            }
            Colaborador selecionado = (Colaborador) JOptionPane.showInputDialog(
                this,
                "Selecione colaborador:",
                "Associar Colaborador",
                JOptionPane.QUESTION_MESSAGE,
                null,
                colaboradores.toArray(),
                t.getColaborador()
            );
            if (selecionado != null) {
                sistema.associarTarefaColaborador(tarefaId, selecionado.getId());
                atualizarTarefas(null,null,null);
            }
        });
        painelBotoes.add(btnAssociarColaborador);

        panel.add(painelBotoes, BorderLayout.SOUTH);
        return panel;
    }

    private void abrirDialogTarefa(Tarefa tarefa) {
        JDialog dialog = new JDialog(this, tarefa == null ? "Adicionar Tarefa" : "Editar Tarefa", true);
        dialog.setSize(400, 300);
        dialog.setLocationRelativeTo(this);
        dialog.setLayout(new GridLayout(6, 2, 5, 5));
        JTextField txtTitulo = new JTextField();
        JTextArea txtDescricao = new JTextArea(3, 20);
        JComboBox<Categoria> cbCategoria = new JComboBox<>();
        sistema.listarCategorias().forEach(cbCategoria::addItem);

        if (tarefa != null) {
            txtTitulo.setText(tarefa.getTitulo());
            txtDescricao.setText(tarefa.getDescricao());
            if (tarefa.getCategoria() != null) {
                cbCategoria.setSelectedItem(tarefa.getCategoria());
            }
        }

        dialog.add(new JLabel("Título:"));
        dialog.add(txtTitulo);
        dialog.add(new JLabel("Descrição:"));
        dialog.add(new JScrollPane(txtDescricao));
        dialog.add(new JLabel("Categoria:"));
        dialog.add(cbCategoria);

        JButton btnSalvar = new JButton("Salvar");
        btnSalvar.addActionListener(e -> {
            String titulo = txtTitulo.getText().trim();
            String descricao = txtDescricao.getText().trim();
            Categoria categoria = (Categoria) cbCategoria.getSelectedItem();
            if (titulo.isEmpty() || descricao.isEmpty() || categoria == null) {
                JOptionPane.showMessageDialog(dialog, "Preencha todos os campos.");
                return;
            }
            try {
                if (tarefa == null) {
                    sistema.criarTarefa(titulo, descricao, categoria.getId());
                } else {
                    sistema.atualizarTarefa(tarefa.getId(), titulo, descricao, categoria.getId());
                }
                atualizarTarefas(null,null,null);
                dialog.dispose();
            } catch (Exception ex) {
                JOptionPane.showMessageDialog(dialog, "Erro: " + ex.getMessage());
            }
        });

        JButton btnCancelar = new JButton("Cancelar");
        btnCancelar.addActionListener(e -> dialog.dispose());

        dialog.add(btnSalvar);
        dialog.add(btnCancelar);

        dialog.setVisible(true);
    }

    private void atualizarCategorias() {
        modelCategorias.clear();
        sistema.listarCategorias().forEach(modelCategorias::addElement);
    }

    private void atualizarColaboradores() {
        modelColaboradores.clear();
        sistema.listarColaboradores().forEach(modelColaboradores::addElement);
    }

    private void atualizarTarefas(Integer colaboradorId, Integer categoriaId, StatusTarefa status) {
        modelTarefas.setRowCount(0);
        List<Tarefa> tarefas = sistema.listarTarefas(colaboradorId, categoriaId, status);
        for (Tarefa t : tarefas) {
            modelTarefas.addRow(new Object[]{
                t.getId(),
                t.getTitulo(),
                t.getDescricao(),
                t.getStatus(),
                t.getCategoria() != null ? t.getCategoria().getNome() : "",
                t.getColaborador() != null ? t.getColaborador().getNome() : ""
            });
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            SistemaControleTarefasGUI gui = new SistemaControleTarefasGUI();
            gui.setVisible(true);
        });
    }
}
