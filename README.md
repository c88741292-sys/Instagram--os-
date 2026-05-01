    return (
      <div style={{ height: "100vh", background: "#0A0A0A" }}>
        <ChatModule module={activeModule} onBack={() => setActiveModule(null)} />
      </div>
    );
  }

  return (
    <div style={{
      minHeight: "100vh", background: "#0A0A0A",
      fontFamily: "'DM Mono', 'Courier New', monospace",
      display: "flex", flexDirection: "column"
    }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400;500&display=swap');
        @keyframes fadeUp { from { opacity:0; transform:translateY(16px) } to { opacity:1; transform:translateY(0) } }
        @keyframes pulse { 0%,100% { opacity:0.4 } 50% { opacity:1 } }
        @keyframes scanline { 0% { transform:translateY(-100%) } 100% { transform:translateY(100vh) } }
        * { box-sizing:border-box; margin:0; padding:0 }
        ::-webkit-scrollbar { width:4px }
        ::-webkit-scrollbar-thumb { background:#222 }
      `}</style>

      {/* Scanline effect */}
      <div style={{
        position: "fixed", top: 0, left: 0, right: 0, bottom: 0,
        pointerEvents: "none", zIndex: 100, overflow: "hidden", opacity: 0.03
      }}>
        <div style={{
          position: "absolute", width: "100%", height: "2px",
          background: "rgba(255,255,255,0.8)",
          animation: "scanline 8s linear infinite"
        }} />
      </div>

      {/* Grid background */}
      <div style={{
        position: "fixed", inset: 0, pointerEvents: "none",
        backgroundImage: "linear-gradient(rgba(255,255,255,0.015) 1px,transparent 1px),linear-gradient(90deg,rgba(255,255,255,0.015) 1px,transparent 1px)",
        backgroundSize: "40px 40px"
      }} />

      <div style={{ position: "relative", zIndex: 1, padding: "40px 24px 60px", maxWidth: "520px", margin: "0 auto", width: "100%" }}>

        {/* Header */}
        <div style={{ animation: "fadeUp 0.6s ease", marginBottom: "40px" }}>
          <div style={{ display: "flex", alignItems: "center", gap: "10px", marginBottom: "20px" }}>
            <div style={{
              width: "40px", height: "40px", borderRadius: "10px",
              background: "linear-gradient(135deg, #FF6B35, #7C3AED)",
              display: "flex", alignItems: "center", justifyContent: "center",
              fontSize: "18px"
            }}>â—ˆ</div>
            <div>
              <div style={{ fontSize: "10px", color: "#555", letterSpacing: "0.15em" }}>CLAUDE-POWERED</div>
              <div style={{ fontSize: "16px", fontWeight: 700, color: "#F0F0F0", letterSpacing: "0.04em" }}>INSTAGRAM OS</div>
            </div>
            <div style={{
              marginLeft: "auto", display: "flex", alignItems: "center", gap: "6px",
              background: "#0F1A0F", border: "1px solid #1A3A1A", borderRadius: "20px",
              padding: "5px 10px", fontSize: "9px", color: "#4ADE80", letterSpacing: "0.1em"
            }}>
              <div style={{ width: "5px", height: "5px", borderRadius: "50%", background: "#4ADE80", animation: "pulse 2s infinite" }} />
              5 SPECIALISTS ONLINE
            </div>
          </div>
          <div style={{ fontSize: "11px", color: "#555", lineHeight: 1.8, letterSpacing: "0.03em" }}>
            Your complete AI-powered Instagram operation. Select a specialist to get started.
          </div>
        </div>

        {/* Module Grid */}
        <div style={{ display: "flex", flexDirection: "column", gap: "12px" }}>
          {MODULES.map((mod, i) => (
            <button
              key={mod.id}
              onClick={() => setActiveModule(mod)}
              onMouseEnter={() => setHoveredId(mod.id)}
              onMouseLeave={() => setHoveredId(null)}
              style={{
                animation: `fadeUp ${0.5 + i * 0.08}s ease both`,
                background: hoveredId === mod.id ? `linear-gradient(135deg, ${mod.color}12, ${mod.accent}06)` : "#0D0D0D",
                border: `1px solid ${hoveredId === mod.id ? mod.color + "50" : "#1E1E1E"}`,
                borderRadius: "14px", padding: "18px 20px", cursor: "pointer",
                textAlign: "left", transition: "all 0.25s ease",
                transform: hoveredId === mod.id ? "translateX(4px)" : "none"
              }}
            >
              <div style={{ display: "flex", alignItems: "center", gap: "14px" }}>
                <div style={{
                  width: "44px", height: "44px", borderRadius: "10px", flexShrink: 0,
                  background: `linear-gradient(135deg, ${mod.color}20, ${mod.accent}12)`,
                  border: `1px solid ${mod.color}35`,
                  display: "flex", alignItems: "center", justifyContent: "center",
                  fontSize: "20px", color: mod.color,
                  transition: "all 0.25s",
                  boxShadow: hoveredId === mod.id ? `0 0 16px ${mod.color}25` : "none"
                }}>{mod.icon}</div>
                <div style={{ flex: 1, minWidth: 0 }}>
                  <div style={{
                    fontSize: "12px", fontWeight: 700, color: "#E0E0E0",
                    letterSpacing: "0.08em", marginBottom: "4px"
                  }}>
                    {mod.label.toUpperCase()}
                    <span style={{
                      marginLeft: "8px", fontSize: "9px", color: mod.color,
                      background: mod.color + "18", borderRadius: "4px",
                      padding: "2px 6px", letterSpacing: "0.1em"
                    }}>SPECIALIST</span>
                  </div>
                  <div style={{ fontSize: "10px", color: "#555", letterSpacing: "0.04em", lineHeight: 1.5 }}>
                    {mod.id === "strategy" && "Growth planning Â· Content calendars Â· Positioning"}
                    {mod.id === "community" && "DMs Â· Comments Â· Outreach Â· Crisis management"}
                    {mod.id === "content" && "Captions Â· Reels Â· Carousels Â· Hashtags"}
                    {mod.id === "analytics" && "Metrics Â· Performance Â· Benchmarking Â· Insights"}
                    {mod.id === "research" && "Trends Â· Algorithm Â· Competitors Â· Intelligence"}
                  </div>
                </div>
                <div style={{
                  fontSize: "16px", color: hoveredId === mod.id ? mod.color : "#333",
                  transition: "all 0.25s",
                  transform: hoveredId === mod.id ? "translateX(3px)" : "none"
                }}>â†’</div>
              </div>
            </button>
          ))}
        </div>

        {/* Footer */}
        <div style={{ marginTop: "36px", textAlign: "center", animation: "fadeUp 1s ease" }}>
          <div style={{ fontSize: "9px", color: "#333", letterSpacing: "0.15em" }}>
            POWERED BY CLAUDE Â· ANTHROPIC Â· v2.0
          </div>
        </div>
      </div>
    </div>
  );
}
