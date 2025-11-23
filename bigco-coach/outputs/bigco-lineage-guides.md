
# BigCo Lineage Guides for API Design

## Guide 1: acknowledge change as the baseline
Richard Price’s lesson  
Systems have always lived inside shifting social, technical, and economic environments. We tend to design as if the world were stable, which is a quiet form of wishful thinking. Good API design starts by assuming conditions will change and by building the surface area where change can occur without tearing the system apart.  
A stable world is the exception, change is the rule, design for the rule.

## Guide 2: expect the unexpected
Frederick Jones’s lesson  
Real environments are messy. Inputs arrive out of order, clients behave unpredictably, integration partners misread specs, and unexpected workflows emerge once the system is in motion. Jones reminds us that elegant models often fail in the field unless they make room for surprise.  
A robust API is not built to handle every scenario, it is built to survive the ones no one predicted.

## Guide 3: build shared understanding before building systems
Reginald Fessenden’s lesson  
Most failures in software are communication failures that happen to take technical form. Misaligned vocabulary, unexamined workflow differences, shallow domain knowledge, and premature code are symptoms of missing conversation.  
Shared language beats clever architecture, if we do not agree on meaning, we will not agree on behavior.

## Guide 4: explore before committing
Leona Woods’s lesson  
Early experiments reveal flaws long before the code would. Woods worked in environments where uncertainty was dangerous, and her approach scales well to modern API practice. Model early, test assumptions early, and let small experiments reduce the cost of being wrong.  
Prototypes and mock interactions should precede the first line of production code, learning early is cheaper than repairing late.

# How to use these guides in API design work

## During domain discovery
Use Guide 3 to anchor conversations. Define terms, map workflows, and challenge assumptions before any story, ALPS profile, or schema is drafted.

## During story writing
Use Guide 1 and Guide 2. Look for places where the story assumes stability. Add affordances that allow for new conditions or new actors.

## During ALPS modeling
Guide 4 becomes central. Treat descriptors as experiments, iterate quickly, consider which parts of the model reflect stable semantics and which reflect evolving practice.

## During interface definition
Revisit all four guides, meaning first, exploration early, tolerance for surprise, expectation of change.

## During long term stewardship
Guide 1 is the governing principle, every API will outlive its assumptions. The work is to keep the system coherent as the world moves around it.

