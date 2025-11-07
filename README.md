# Go/No-Go Response Inhibition Trainer with Novel Stimuli

A web-based cognitive training tool that implements the stop-signal paradigm for measuring and training response inhibition abilities. This implementation uses **novel stimuli** on each trial to minimize task-specific learning strategies and maximize training benefits.

## Key Features

### Novel Stimuli Design
- Each trial presents a **unique visual stimulus** (randomly generated shapes, colors, and orientations)
- Prevents participants from developing automated responses to familiar patterns
- Forces engagement with the actual task demands rather than memorized responses
- Shapes include: circles, squares, triangles, diamonds, stars, and hexagons
- Varied colors and rotations on every trial

### Timing Specifications
- **Response window:** 500ms maximum
- **Stop signal delay:** Randomly varies between 100-450ms after stimulus onset
- **White circle indicator:** Appears at stimulus onset on no-go trials
- **Red circle (stop signal):** Indicates participant must inhibit response

### Task Structure

#### Block 1: Practice Block (20 trials)
- All GO trials
- Helps participants learn the basic response task
- Familiarizes users with the response window and stimulus types

#### Block 2: Experimental Block (40 trials)
- 30 GO trials: Respond as quickly as possible
- 10 NO-GO trials: Inhibit response when circle turns red
- Randomized trial order

## How It Works

### GO Trials
1. Fixation cross appears (500-1000ms)
2. Novel stimulus appears with directional arrow (left/right)
3. Participant presses corresponding arrow key within 500ms
4. Feedback provided (correct/wrong/timeout)

### NO-GO Trials
1. Fixation cross appears (500-1000ms)
2. Novel stimulus appears with white circle overlay
3. White circle turns **RED** between 100-450ms
4. Participant must **inhibit** their response when they see red
5. Feedback provided based on inhibition success

## Data Output Format

The trainer outputs tab-separated data with the following columns:

| Column | Meaning |
|--------|---------|
| 1 | Trial type (go or nogo) |
| 2 | Required response (left or right) |
| 3 | Stop signal timing (ms after stimulus, or 0 for go trials) |
| 4 | Response time 1 (ms) |
| 5 | Status 1 (1=correct, 2=wrong, 3=timeout) |
| 6 | Response time 2 (only in no-go trials, ms) |
| 7 | Status 2 (only in no-go trials; 1=correct, 2=wrong, 3=timeout) |
| 8 | Trial correct (1=correct, 0=incorrect) |

### Status Codes
- **1:** Correct response
- **2:** Wrong response (wrong key or failed to inhibit)
- **3:** Timeout (no response within 500ms)

### Example Data Line
```
nogo    right   325     0       0       0       1       1
```
This indicates:
- NO-GO trial
- Required response would have been right arrow
- Stop signal appeared 325ms after stimulus
- No response before stop signal (RT1=0, Status1=0)
- No response after stop signal (RT2=0, Status2=1 = correctly inhibited)
- Trial was correct (1)

## Usage

1. **Open the trainer:** Open `index.html` in a modern web browser
2. **Read instructions:** Review the task instructions on the welcome screen
3. **Complete Block 1:** Practice with all GO trials
4. **Complete Block 2:** Experimental block with mixed GO/NO-GO trials
5. **Review results:** See your accuracy and inhibition failure rate
6. **Download data:** Export your performance data for analysis

## Key Metrics

### Inhibition Failure Rate
The primary measure of response inhibition ability:
- **Lower rate = Better inhibition control**
- Calculated as: (Failed NO-GO trials / Total NO-GO trials) × 100%
- Typical ranges: 10-30% for healthy adults

### GO Trial Accuracy
Measures basic task performance:
- Should be high (>90%) if participant understands the task
- Low accuracy suggests issues with task comprehension or attention

## Scientific Background

This task is based on the stop-signal paradigm developed by Logan and colleagues:

- **Logan, G.D., Cowan, W.B., & Davis, K.A. (1984).** On the Ability to Inhibit Simple and Choice Reaction Time Responses: A Model and a Method. *Journal of Experimental Psychology: Human Perception and Performance, 10*, 276-291.

- **Logan, G. D. (2015).** The point of no return: A fundamental limit on the ability to control thought and action. *Quarterly Journal of Experimental Psychology, 68*, 833-857.

- **Verbruggen, F., & Logan, G.D. (2008).** Response Inhibition in the Stop-Signal Paradigm. *Trends in Cognitive Sciences, 12(11)*, 418-424.

## Why Novel Stimuli?

Traditional go/no-go tasks use the same stimuli repeatedly, which can lead to:
- **Automatic responding:** Participants memorize stimulus-response mappings
- **Task-specific strategies:** Performance doesn't generalize to real-world inhibition
- **Reduced engagement:** Repetitive stimuli become boring

By using **novel stimuli** on each trial:
- ✓ Maintains attention and engagement
- ✓ Prevents automatic responding
- ✓ Measures genuine inhibitory control rather than learned patterns
- ✓ Better reflects real-world cognitive demands

## Technical Details

- **Pure HTML/JavaScript:** No external dependencies required
- **Client-side only:** All data processing happens in the browser
- **Browser compatibility:** Works with all modern browsers (Chrome, Firefox, Safari, Edge)
- **Responsive design:** Adapts to different screen sizes

## Analysis Suggestions

For analyzing the output data:

1. **Focus on NO-GO trials** (lines starting with "nogo")
2. **Calculate inhibition failure rate:** Count trials where column 8 = 0
3. **Examine stop signal delay effects:** Group by column 3 to see if earlier/later signals affect performance
4. **Check response times:** Analyze column 4 for GO trials to ensure participants are responding quickly

## License

This implementation is provided for educational and research purposes.

## Contact

For questions about the task design or implementation, please refer to the scientific literature cited above.
