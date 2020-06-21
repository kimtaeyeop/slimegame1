# slimegame1

// Study01.java
 
package study;
 
import java.awt.Font;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.Enumeration;
 
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.UIManager;
import javax.swing.plaf.FontUIResource;
 
public class Study01 {
 
    // 전역 변수 선언
    static JLabel lbl, lbl2, imgLbl, imgLbl2;
    static ImageIcon bsImg, rsImg;
    static JButton btn1, btn2;
 
    // 슬라임과 인간 객체 생성
    static BlueSlime bs1 = new BlueSlime("슬라삐");
    static RedSlime rs1 = new RedSlime("슬라디");
    static Human h = new Human("알렉스");
 
    public static void main(String[] args) {
 
        // [start] 디자인 코드
 
        // 모든 글꼴 통일
        Enumeration<Object> keys = UIManager.getDefaults().keys();
        while (keys.hasMoreElements()) {
            Object key = keys.nextElement();
            Object value = UIManager.get(key);
            if (value instanceof FontUIResource)
                UIManager.put(key, new FontUIResource("굴림", Font.PLAIN, 14));
        }
 
        // [start] 프레임 설정(게임을 표시하는 윈도우입니다)
        JFrame frm = new JFrame();
        frm.setTitle("슬라임 퇴치하기");
        frm.setSize(350, 350);
        frm.setLocationRelativeTo(null);
        frm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frm.getContentPane().setLayout(null);
        // [end] 프레임 설정
 
        // [start] 버튼 설정(버튼을 눌러서 슬라임을 공격합니다)
        btn1 = new JButton(bs1.name);
        btn2 = new JButton(rs1.name);
        btn1.setBounds(30, 170, 122, 30);
        btn2.setBounds(182, 170, 122, 30);
        frm.getContentPane().add(btn1);
        frm.getContentPane().add(btn2);
        // [end] 버튼 설정
 
        // 라벨 설정(전투 정보 표시)
        lbl = new JLabel();
        lbl.setBounds(30, 210, 274, 50);
        lbl.setText("게임을 시작합니다");
        lbl.setHorizontalAlignment(JLabel.CENTER); // 수평 가운데 정렬
        frm.getContentPane().add(lbl);
 
        // 라벨2 설정(전투 정보 표시2)
        lbl2 = new JLabel();
        lbl2.setBounds(30, 240, 274, 50);
        lbl2.setText(h.name + "의 체력은 " + h.hp + "입니다");
        lbl2.setHorizontalAlignment(JLabel.CENTER); // 수평 가운데 정렬
        frm.getContentPane().add(lbl2);
 
        // [start] 이미지 라벨 생성(블루슬라임 그림을 표시)
        imgLbl = new JLabel();
        bsImg = new ImageIcon(Study01.class.getResource("/study/img/slime(blue).png"));
        imgLbl.setIcon(bsImg);
        imgLbl.setBounds(30, 30, 122, 130);
        imgLbl.setHorizontalAlignment(JLabel.CENTER);
        frm.getContentPane().add(imgLbl);
        // [end]
 
        // [start] 이미지 라벨2 생성(레드슬라임 그림을 표시)
        imgLbl2 = new JLabel();
        rsImg = new ImageIcon(Study01.class.getResource("/study/img/slime(red).png"));
        imgLbl2.setIcon(rsImg);
        imgLbl2.setBounds(182, 30, 122, 130);
        imgLbl2.setHorizontalAlignment(JLabel.CENTER);
        frm.getContentPane().add(imgLbl2);
        // [end]
 
        // 프레임이 보이도록 설정
        frm.setVisible(true);
 
        // [end]
 
        // 버튼을 눌렀을때
        btn1.addActionListener(event -> {
 
            battle(bs1);
 
        });
 
        btn2.addActionListener(event -> {
 
            battle(rs1);
 
        });
 
    }
 
    public static void battle(Slime s) {
    	int randomNum = (int)(Math.random()*3);
    	if(randomNum == 0) {
    		lbl.setText(h.name + "의 공격이 빗나갔다");
    	}else {
       
    	
    	h.attack(s);
    	}
    	
        if (s instanceof BlueSlime) {
        	randomNum = (int)(Math.random()*3);
        	if(randomNum == 0) {
            ((BlueSlime) s).heal(s);
 
        } else {
            s.attack(h);
        }
        }else {
        	randomNum = (int)(Math.random()*3);
        	if(randomNum == 0) {
            ((RedSlime) s).attack2(h);
        	}else {
        		s.attack(h);
        	}
        }
        // 슬라임이 모두 죽으면 게임 클리어
        if (bs1.hp < 1 && rs1.hp < 1) {
 
            JOptionPane.showMessageDialog(lbl2, "Game Clear!");
            System.exit(0);
        }
 
    }
    }
