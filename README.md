import javax.sound.sampled.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.io.File;
import java.io.IOException;
import javax.swing.*;

public class VirtualPiano extends JFrame implements KeyListener {
    public VirtualPiano() {
        setTitle("Virtual Piano 🎹");
        setSize(400, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
        addKeyListener(this);
    }

    private void playSound(String soundFile) {
        try {
            File file = new File("sounds/" + soundFile);
            AudioInputStream audioStream = AudioSystem.getAudioInputStream(file);
            Clip clip = AudioSystem.getClip();
            clip.open(audioStream);
            clip.start();
        } catch (UnsupportedAudioFileException | IOException | LineUnavailableException e) {
            System.err.println("Error playing sound: " + e.getMessage());
        }
    }

    @Override
    public void keyPressed(KeyEvent e) {
        switch (e.getKeyCode()) {
            case KeyEvent.VK_A: playSound("C.wav"); break; // 'A' for C note
            case KeyEvent.VK_S: playSound("D.wav"); break; // 'S' for D note
            case KeyEvent.VK_D: playSound("E.wav"); break; // 'D' for E note
            case KeyEvent.VK_F: playSound("F.wav"); break; // 'F' for F note
            case KeyEvent.VK_G: playSound("G.wav"); break; // 'G' for G note
            case KeyEvent.VK_H: playSound("A.wav"); break; // 'H' for A note
            case KeyEvent.VK_J: playSound("B.wav"); break; // 'J' for B note
            default: System.out.println("Press A, S, D, F, G, H, or J for piano notes.");
        }
    }

    @Override
    public void keyReleased(KeyEvent e) { }
    
    @Override
    public void keyTyped(KeyEvent e) { }

    public static void main(String[] args) {
        new VirtualPiano();
    }
}
