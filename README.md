## 📬 Laravel 10 Cron Job Email Example
This Laravel 10 project shows how to send emails every minute using a cron job. No queues, no complex setup — just a clean scheduled command and a Blade email view.

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
