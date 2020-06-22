# Example
```cs
using System;
using System.Diagnostics;
using System.Globalization;
using Trainer;
using Trainer.Common;


namespace App_Hacker
{
	class Program
	{
		public static void Main(string[] args)
		{
            Console.WriteLine("Digite o nome do processo");
            // Process Name
            var processo_nome = Console.ReadLine();
            var process_select = Process.GetProcessesByName(processo_nome);
            if (process_select.Length != 0)
            {
                // first process
                var process = process_select[0];
                var trainer = new Cheat_Manager(process);
                Console.WriteLine("Digite o valor do address");
                // hexadecimal = F0
                var address_hex = Console.ReadLine();
                var address_int = 0;
                if (int.TryParse(address_hex, NumberStyles.HexNumber, CultureInfo.InvariantCulture, out address_int))
                {
                    Console.WriteLine("Digite o valor para escrever no address");
                    var value_ = Console.ReadLine();
                    var result = 0;
                    if (int.TryParse(value_, out result))
                    {
                        var flag = trainer.WriteMemory(new IntPtr(address_int), Value_Type._4Bytes(result));
                        if (flag)
                        {
                            Console.WriteLine("Successo");
                        }
                        else
                        {
                            Console.WriteLine("Erro ao mudar o valor na memória");
                        }
                    }
                    else
                    {
                        Console.WriteLine("Valor invalido");
                    }
                }
                else
                {
                    Console.WriteLine("Address invalida");
                }
            }
            else
            {
                Console.WriteLine("Não existe nenhum processo");
            }
            Console.ReadLine();
		}
	}
}
```
