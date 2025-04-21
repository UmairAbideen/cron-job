## 📬 Laravel 10 Cron Job Email Example
This Laravel 10 project shows how to send emails every minute using a cron job. No queues, no complex setup — just a clean scheduled command and a Blade email view.

## ⏰ Why Use a Cron Job?
Cron jobs are used to automate recurring tasks at scheduled intervals without manual triggering. In Laravel, this is useful when you want actions (like sending emails) to run consistently — for example, every minute, hour, or day — even if no user is interacting with the app.

Common use cases:

- Send scheduled emails (like reports, reminders, digests)
- Clean up old data or logs
- Generate or backup files

## 📝 Steps to Set Up a Cron Job in Laravel (Without Queue)

1. Create a new Artisan command
This command will contain the logic to send the email.

2. Write the email logic
Inside the command, define how and what email should be sent.

3. Create an email Blade view (optional)
Design the content of the email that will be sent.

4. Register the command in Laravel's scheduler
Add your command to the schedule() method in the Console Kernel, and define when it should run (like every minute).

5. Manually test the scheduler
Run Laravel’s scheduler once via terminal to see if it triggers the email command correctly.

6. Set up system cron (on production)
Add a cron entry to your OS to run Laravel’s schedule:run every minute. This lets the framework check and execute any scheduled tasks.


## 📄 Command Class (SendEmailCommand.php)

```bash
public function handle()
{
    $data = [
        'subject' => 'Email via Cron Job',
        'title' => 'Scheduled Email',
        'body' => 'Testing Email.',
        'email' => 'you@example.com',
    ];

    Mail::send('message', $data, function ($message) use ($data) {
        $message->to($data['email']);
        $message->subject($data['subject']);
    });
}
```
## 🖼️ Blade View (resources/views/message.blade.php)

```bash

<h1>{{ $title }}</h1>
<p>{{ $body }}</p>

```

## 🕒 Kernel Schedule (App\Console\Kernel.php)
```bash
protected function schedule(Schedule $schedule)
{
    $schedule->command('send:email')->everyMinute();
}

⚙️ Artisan Commands
```bash
php artisan make:command SendEmailCommand
php artisan send:email         # To test manually
php artisan schedule:run       # To simulate cron run manually
