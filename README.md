# Практическая работа №4: Циклические конструкции в C# (while, do-while, for) и разработка консольной RPG
# Подземные тайны
## Выполнили студенты группы П25-2.1 Карпухин Дмитрий и Есин Данила
---
<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/1.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/2.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/3.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/4.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/5.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/6.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/7.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/8.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/9.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/10.png">
</picture>

<picture>
  <img src="https://github.com/Karpukhin-D/Task-4/blob/main/game/11.png">
</picture>

```csharp
using System;

class Program
{
    static void Main()
    {
        const int maxHp = 100;
        const int maxOxygen = 10;
        const int maxBattery = 6;
        const int maxRecoveryUses = 3;
        const int specialCost = 2;
        const int barLength = 20;

        int playerHp = maxHp;
        int oxygen = maxOxygen;
        int battery = maxBattery;
        int recoveryUses = maxRecoveryUses;

        Random random = new Random();

        Console.ForegroundColor = ConsoleColor.DarkYellow;
        Console.WriteLine("========================================");
        Console.WriteLine("         ПОДЗЕМНЫЕ ТАЙНЫ");
        Console.WriteLine("========================================");
        Console.ResetColor();

        Console.WriteLine("Вы — шахтер-ликвидатор.");
        Console.WriteLine("В глубинах шахты произошёл обвал.");
        Console.WriteLine("Вам необходимо пройти три опасные зоны.");
        Console.WriteLine("Главная задача — выжить и выбраться наружу.");
        Console.WriteLine();

        for (int wave = 1; wave <= 3; wave++)
        {
            string enemyName;
            int enemyHp;
            int enemyMinDamage;
            int enemyMaxDamage;

            if (wave == 1)
            {
                enemyName = "Ядовитый паук глубин";
                enemyHp = 55;
                enemyMinDamage = 8;
                enemyMaxDamage = 12;
            }
            else if (wave == 2)
            {
                enemyName = "Каменный голем";
                enemyHp = 75;
                enemyMinDamage = 11;
                enemyMaxDamage = 16;
            }
            else
            {
                enemyName = "Королева гнезда";
                enemyHp = 105;
                enemyMinDamage = 14;
                enemyMaxDamage = 20;
            }

            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine();
            Console.WriteLine("========================================");
            Console.WriteLine($"                ВОЛНА {wave}");
            Console.WriteLine("========================================");
            Console.WriteLine($"Появился противник: {enemyName}");
            Console.WriteLine($"Здоровье противника: {enemyHp}");
            Console.ResetColor();

            while (playerHp > 0 && enemyHp > 0 && oxygen > 0)
            {
                int hpBlocks = playerHp * barLength / maxHp;

                Console.WriteLine();
                Console.WriteLine("------------- СОСТОЯНИЕ ---------------");

                Console.Write("Здоровье  [");

                for (int i = 0; i < hpBlocks; i++)
                {
                    Console.Write("#");
                }

                for (int i = hpBlocks; i < barLength; i++)
                {
                    Console.Write("-");
                }

                Console.WriteLine($"] {playerHp}/{maxHp}");

                int oxygenBlocks = oxygen * barLength / maxOxygen;

                Console.Write("Кислород  [");

                for (int i = 0; i < oxygenBlocks; i++)
                {
                    Console.Write("#");
                }

                for (int i = oxygenBlocks; i < barLength; i++)
                {
                    Console.Write("-");
                }

                Console.WriteLine($"] {oxygen}/{maxOxygen}");

                int batteryBlocks = battery * barLength / maxBattery;

                Console.Write("Батарея   [");

                for (int i = 0; i < batteryBlocks; i++)
                {
                    Console.Write("#");
                }

                for (int i = batteryBlocks; i < barLength; i++)
                {
                    Console.Write("-");
                }

                Console.WriteLine($"] {battery}/{maxBattery}");

                Console.WriteLine($"Баллоны кислорода: {recoveryUses}");
                Console.WriteLine($"Противник: {enemyName} | HP: {enemyHp}");
                Console.WriteLine("----------------------------------------");

                int action;
                bool isValid;

                do
                {
                    Console.WriteLine();
                    Console.WriteLine("Выберите действие:");
                    Console.WriteLine("1 — Удар киркой");
                    Console.WriteLine("2 — Мощный разряд фонаря");
                    Console.WriteLine("3 — Защитная стойка");
                    Console.WriteLine("4 — Использовать баллон кислорода");
                    Console.Write("Ваш выбор: ");

                    isValid = int.TryParse(Console.ReadLine(), out action) && action >= 1 && action <= 4;

                    if (!isValid)
                    {
                        Console.ForegroundColor = ConsoleColor.Red;
                        Console.WriteLine("Ошибка! Введите число от 1 до 4.");
                        Console.ResetColor();
                    }

                } while (!isValid);

                bool isDefending = false;

                switch (action)
                {
                    case 1:
                        int basicDamage = random.Next(20, 26);

                        enemyHp -= basicDamage;

                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine($"Вы ударили киркой и нанесли {basicDamage} урона!");
                        Console.ResetColor();
                        break;

                    case 2:
                        if (battery < specialCost)
                        {
                            Console.ForegroundColor = ConsoleColor.Red;
                            Console.WriteLine("Недостаточно энергии фонаря!");
                            Console.ResetColor();

                            continue;
                        }

                        int specialDamage = random.Next(30, 41);

                        enemyHp -= specialDamage;
                        battery -= specialCost;

                        Console.ForegroundColor = ConsoleColor.Cyan;
                        Console.WriteLine($"Мощный разряд фонаря нанёс {specialDamage} урона!");
                        Console.WriteLine($"Потрачено батареи: {specialCost}");
                        Console.ResetColor();
                        break;

                    case 3:
                        isDefending = true;

                        Console.ForegroundColor = ConsoleColor.Yellow;
                        Console.WriteLine("Вы встали в защитную стойку.");
                        Console.WriteLine("Получаемый урон будет уменьшен вдвое.");
                        Console.ResetColor();
                        break;

                    case 4:
                        if (recoveryUses <= 0)
                        {
                            Console.ForegroundColor = ConsoleColor.Red;
                            Console.WriteLine("Баллоны кислорода закончились!");
                            Console.ResetColor();

                            continue;
                        }

                        int oxygenBefore = oxygen;

                        oxygen += 3;

                        if (oxygen > maxOxygen)
                        {
                            oxygen = maxOxygen;
                        }

                        recoveryUses--;

                        Console.ForegroundColor = ConsoleColor.Blue;
                        Console.WriteLine("Вы использовали баллон кислорода.");
                        Console.WriteLine($"Кислород: {oxygenBefore} -> {oxygen}");
                        Console.WriteLine($"Осталось баллонов: {recoveryUses}");
                        Console.ResetColor();
                        break;
                }

                if (enemyHp <= 0)
                {
                    enemyHp = 0;

                    Console.ForegroundColor = ConsoleColor.Green;
                    Console.WriteLine();
                    Console.WriteLine($"*** {enemyName} ПОВЕРЖЕН! ***");
                    Console.ResetColor();

                    break;
                }

                int enemyDamage = random.Next(enemyMinDamage, enemyMaxDamage + 1);

                if (isDefending)
                {
                    enemyDamage = enemyDamage / 2;
                    Console.WriteLine("Защита уменьшила получаемый урон вдвое.");
                }

                playerHp -= enemyDamage;

                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine($"{enemyName} нанёс вам {enemyDamage} урона.");
                Console.ResetColor();

                if (playerHp <= 0)
                {
                    playerHp = 0;

                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine();
                    Console.WriteLine("Вы получили смертельный урон.");
                    Console.ResetColor();

                    break;
                }

                oxygen--;

                Console.ForegroundColor = ConsoleColor.DarkCyan;
                Console.WriteLine($"Подземелье расходует кислород. Осталось: {oxygen}");
                Console.ResetColor();

                if (oxygen <= 0)
                {
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine("Кислород закончился!");
                    Console.ResetColor();

                    break;
                }
            }

            if (playerHp <= 0 || oxygen <= 0)
            {
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine();
                Console.WriteLine("========================================");
                Console.WriteLine("             ПОРАЖЕНИЕ");
                Console.WriteLine("========================================");
                Console.ResetColor();

                break;
            }

            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine();
            Console.WriteLine($"Волна {wave} завершена!");
            Console.WriteLine("Вы идёте глубже в шахту...");
            Console.ResetColor();
        }

        if (playerHp > 0 && oxygen > 0)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine();
            Console.WriteLine("========================================");
            Console.WriteLine("              ПОБЕДА!");
            Console.WriteLine("========================================");
            Console.WriteLine("Все три противника побеждены.");
            Console.WriteLine("Шахтёр выбрался из подземелья!");
            Console.ResetColor();
        }

        Console.WriteLine();
        Console.WriteLine("Нажмите Enter для выхода.");
        Console.ReadLine();
    }
}
```
