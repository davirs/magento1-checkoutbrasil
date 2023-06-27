# Módulo Magento 1
## Máscara e validação de CPF e CNPJ

Módulo para mascara e validação de CPF e CNPJ feito com base no Magento 1.9.4.*

Você pode instalar via [modgit](https://github.com/jreinke/modgit) usando o comando abaixo.

```
modgit add validaCPF https://github.com/rafaelstz/magento1-validaCPF
```

### License

MIT - [Rafael Corrêa Gomes](https://github.com/rafaelstz)


FIRECHECKOUT:
Após instalar este módulo ele já vai validar os campos do magento.
para funcionar no firecheckout tem que editar o arquivo:
app\design\frontend\base\default\template\rafaelcg\validacpf\customer\widget\taxvat.phtml

para o seguinte código:
<label for="<?= $this->getFieldId('taxvat')?>"<?php if ($this->isRequired()) echo ' class="required"' ?>><?php if ($this->isRequired()) echo '<em>*</em>' ?><?php echo $this->__('CPF/CNPJ') ?></label>
<div class="input-box">
    <input type="text" id="<?= $this->getFieldId('taxvat')?>" name="<?php echo $this->getFieldName('taxvat')?>" value="<?php echo $this->escapeHtml($this->getTaxvat()) ?>" title="<?php echo Mage::helper('core')->quoteEscape($this->__('CPF/CNPJ')) ?>" class="input-text validar-cpf <?php echo $this->helper('customer/address')->getAttributeValidationClass('taxvat') ?>" <?php echo $this->getFieldParams() ?> />
</div>

<script type="text/javascript">
//<![CDATA[
    Validation.add('validar-cpf', '<?= $this->__('O número informado é inválido') ?>', function(v) {return validaCPFCNPJ.init(v,0);});
    document.observe("dom:loaded",() => {
        document.querySelectorAll('[id="<?php echo $this->getFieldId('taxvat')?>"]').forEach(($input) => {
            $input.addEventListener('input', (e) => {
                e.target.value = validaCPFCNPJ.mask(e.target.value);
            }, false)
        });
    })
//]]>
</script>
