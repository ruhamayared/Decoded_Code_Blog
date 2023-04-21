<p>In this blog post, I will create a simple command-line To-Do app in Rust. I will go through the code step-by-step, explaining how each part works. By the end, you will have a basic understanding of Rust and a functioning To-Do app.&nbsp;</p><p><br /><b>Prerequisites:</b><br /></p><ul style="text-align: left;"><li>Basic Rust knowledge</li><li>Rust installed on your computer</li></ul><div><br /><b>Getting Started:</b></div><div>First, let's create a new Rust project:</div><pre><code>cargo new todo_app 
cd todo_app</code></pre>
<p>Now open <code>src/main.rs</code> in your favorite text editor.</p><p></p><br/>
<p><b>Importing Necessary Modules:</b><br />We'll start by importing the necessary modules from the Rust standard library:</p><pre><code>use std::io::{stdin, stdout, Write};
use std::collections::HashMap;</code></pre>
<p>Here's what each module does:</p><p></p><ul style="text-align: left;"><li><code>std::io::stdin</code>: Reads user input from the standard input stream (usually the keyboard).</li><li><code>std::io::stdout</code>: Accesses the standard output stream (usually the console).</li><li><code>std::io::Write</code>: Provides the <code>flush()</code> method for output streams, including stdout.</li><li><code>std::collections::HashMap</code>: Implements the <code>HashMap</code> data structure, a key-value store.</li></ul><p></p>
<div><br /><b>Setting Up the Main Function and Data Structures:</b></div><div>Next, let's define the <code>main</code> function and create the data structures for storing our tasks:</div><div></div><div></div>
<pre><code>fn main() {
    let mut tasks: HashMap<u32 string=""> = HashMap::new();
    let mut task_id_counter: u32 = 1;
</u32></code></pre>
<div>We use a <code>HashMap</code> to store tasks, with a unique identifier (u32) as the key and the task description <code>(String)</code> as the value. We also initialize a <code>task_id_counter</code> to assign unique IDs to tasks as they are added.</div><p></p><br/>
<b>The Main Loop and User Interaction:</b></div><div>Now we'll set up the main loop to display the menu and handle user actions:</div><div></div><p></p>**The Main Loop and User Interaction:**

Now we'll set up the main loop to display the menu and handle user actions:

```rust
loop {
    println!("What would you like to do?");
    println!("1) Add task");
    println!("2) List tasks");
    println!("3) Complete task");
    println!("4) Quit");

    let mut choice = String::new();
    stdin().read_line(&mut choice).unwrap();

```
<p>We use a <code>loop</code> to continually display the menu and read the user's choice. The <code>stdin().read_line(&amp;mut choice)</code> method reads input from the user and stores it in the <code>choice</code> variable.</p>

<p><br /><b>Handling User Actions:</b><br />We will use a match statement to handle the user's actions based on their input.</p><pre><code>        match choice.trim().parse::<u8>() {
</u8></code></pre>
<p>We <code>trim()</code> the user's input to remove any leading or trailing whitespace, and then <code>parse()</code> it as a <code>u8</code> value.</p><br/>

<b>Adding a Task:</b><br />When the user selects "1", we prompt them to enter the task description.</p>            
```rust
            Ok(1) =&gt; {
                let mut task = String::new();
                print!("Enter the task: ");
                stdout().flush().unwrap();
                stdin().read_line(&amp;mut task).unwrap();

                tasks.insert(task_id_counter, task.trim().to_string());
                println!("Task added with ID: {}", task_id_counter);
                task_id_counter += 1;
            }
```

<p></p><p>We read the task description, store it in the <code>tasks Hashmap</code>, increment the <code>task_id_counter</code>, and display a confirmation message.<br /><br /></p><p><b>Listing Tasks:</b><br />When the user selects "2", we list the tasks. We can list the tasks in order by using a <code>Vec</code>.</p>           
```rust
            Ok(2) =&gt; {
                if tasks.is_empty() {
                    println!("No tasks.");
                } else {
                    println!("Tasks:");

                    // Collect tasks into a Vec and sort by task ID
                    let mut sorted_tasks: Vec&lt;(&amp;u32, &amp;String)&gt; = tasks.iter().collect();
                    sorted_tasks.sort_by_key(|&amp;(id, _)| id);

                    // Iterate through the sorted Vec and print the task ID and description
                    for (id, task) in sorted_tasks {
                        println!("{} - {}", id, task);
                    }
                }
            }
```
<p>By using <code>tasks.iter().collect()</code> to create a <code>Vec</code> of references to the tasks, we avoid cloning the data. Then, we use <code>sort_by_key()</code> to sort the <code>Vec</code> based on the task IDs. Finally, we iterate through the sorted <code>Vec</code> to print the tasks in order.</p><p><br />