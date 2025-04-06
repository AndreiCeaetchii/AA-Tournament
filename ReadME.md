
---

# Generous Tit for Tat (GTFT)

### Description

1. **Initial Setup**  
   - The function signature is `strategy(my_history: list[int], opponent_history: list[int], rounds: int | None) -> int`.  
   - Each round, `my_history` and `opponent_history` store all previous moves of the player and opponent (respectively). Each move is an integer: `1` for cooperate, `0` for defect.  
   - `rounds` may be `None` or an integer. Although GTFT can ignore it, some variants might factor it into endgame behavior.

2. **First Move**  
   - If `my_history` is empty (i.e., on the very first round), the strategy **cooperates** by returning `1`.

3. **Tit for Tat Foundation**  
   - In classic Tit for Tat, you simply “echo” the opponent’s last move: cooperate if they cooperated last time, defect if they defected last time.

4. **Generous Twist**  
   - GTFT adds occasional “forgiveness.” Specifically, when the opponent defects in the previous round, this strategy **usually** defects back, **but** occasionally (on a simple pattern, e.g., every Nth time) it cooperates anyway.  
   - Because external randomness isn’t allowed, a deterministic pattern is used (for instance, *every 4th time you would otherwise defect*, cooperate instead).

5. **Move Return**  
   - The function must return `1` (cooperate) or `0` (defect) at every call, reflecting the chosen action for the current round.

### Analysis

- **Niceness**  
  GTFT starts with cooperation and tends to remain cooperative unless provoked, which fosters mutual cooperation with nice or friendly opponents.

- **Retaliation**  
  If the opponent defects, GTFT punishes them in the next round (defecting back). This discourages an opponent from repeatedly exploiting the strategy.

- **Forgiveness**  
  Periodically “forgiving” a defection can prevent endless retaliatory loops. If the opponent is also open to cooperation, GTFT can quickly re-establish cooperation and avoid low-payoff mutual defection.

- **Simplicity & Adaptability**  
  GTFT is straightforward to implement and highly adaptive. Its short memory (it only needs to recall the opponent’s last move or a small pattern) keeps computations minimal.

This combination of **niceness**, **retaliation**, and **forgiveness** often leads to strong results in iterative Prisoner’s Dilemma tournaments.

---
