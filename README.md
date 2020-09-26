# Gerene.DFe.EscPos

[![Nuget count](http://img.shields.io/nuget/v/Gerene.DFe.EscPos.svg)](https://www.nuget.org/packages/Gerene.DFe.EscPos)

Impressão em EscPos, EscBema e EscDaruma para DFes

Atualmente a biblioteca atende os documentos SAT e NFCe.

Funcionamento:
----

O projeto é construído em .Net Standard 2.0 e conta com dois demos (.Net Framework 4.6.2 e .Net Core 3.1).

Exemplo de uso:
```
using (var _printer = new SatPrinter()) //ou new NFCePrinter() para NFCe
{
	_printer.TipoImpressora = PrinterType.Epson; //Epson para EscPos / Bematech para EscBema / Daruma para EscDaruma
	_printer.NomeImpressora = "Nome da impressora";
	_printer.CortarPapel = true;
	_printer.ProdutoDuasLinhas = false;
	_printer.UsarBarrasComoCodigo = false;
	_printer.DocumentoCancelado = false; //Exibe tarja "Documento cancelado na impressão"
	_printer.Logotipo = logotipo_em_bytes; //Impressão do logotipo, não obrigatório

	_printer.Imprimir(string_com_o_conteudo_do_xml); //Imprime o documento fiscal
	
	// para impressão específica do XML de cancelamento de SAT CF-e use:
        //_printer.ImprimirCancelamento(string_com_o_conteudo_do_xml_de_cancelamento);
}
```

Implementando um novo tipo documento:
----

Para ajudar e implementar um novo tipo de documento basta implementar a interface IDFe

```
public interface IDfePrinter : IDisposable
{
	string NomeImpressora { get; set; }
	PrinterType TipoImpressora { get; set; }
	bool CortarPapel { get; set; }
	bool ProdutoDuasLinhas { get; set; }
	bool UsarBarrasComoCodigo { get; set; }
	bool DocumentoCancelado {get; set; }
	byte[] Logotipo { get; set; }

	void Imprimir(string xmlcontent);
}
```

Dependências:
----

Vip.Printer (motor de impressão) - https://github.com/leandrovip/Vip.Printer

ACBr.Net.Sat (desserialização do xml do SAT) - https://github.com/ACBrNet/ACBr.Net.Sat

DFe.Net (desserialização do xml da NFCe) - https://github.com/ZeusAutomacao/DFe.NET

----


A licença do projeto é MIT, o seu uso é livre.
Não garantimos QUALQUER suporte.
