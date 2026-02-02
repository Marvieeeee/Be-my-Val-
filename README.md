    const A = window.AudioContext || window.webkitAudioContext;
    const ac = new A();
    const now = ac.currentTime;

    const o1 = ac.createOscillator();
    const o2 = ac.createOscillator();
    const g = ac.createGain();

    o1.frequency.value = 880; // A5
    o2.frequency.value = 1320; // E6
    o1.type = 'sine';
    o2.type = 'triangle';

    g.gain.setValueAtTime(0, now);
    g.gain.linearRampToValueAtTime(0.08, now + 0.02);
    g.gain.exponentialRampToValueAtTime(0.0001, now + 1.2);

    o1.connect(g);
    o2.connect(g);
    g.connect(ac.destination);

    o1.start(now);
    o2.start(now);
    o1.stop(now + 1.2);
    o2.stop(now + 1.2);
  } catch(e) {
    // Audio may be blocked by browser autoplay policy; ignore
    console.warn("Audio not available:", e);
  }
}
</script>
</body>
</html>
