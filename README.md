# RFM_PROJETO
TESTE AUTOMATIZADO - Login

const { remote } = require('webdriverio');

async function executarTeste() {
    const driver = await remote({
        capabilities: {
            platformName: "Android",
            "appium:deviceName": "Emulador_RFM",
            "appium:app": "/caminho/para/seu/app.apk",
            "appium:automationName": "UiAutomator2"
        }
    });

    // Fluxo de Login
    const campoEmail = await driver.$('~input-email'); // Usando Accessibility ID
    await campoEmail.setValue('colaborador@empresa.com');

    const campoSenha = await driver.$('~input-senha');
    await campoSenha.setValue('1234');

    const botaoEntrar = await driver.$('~btn-entrar');
    await botaoEntrar.click();

    // Validação pós-login (Tela RFM)
    const telaRFM = await driver.$('~dashboard-rfm');
    await telaRFM.waitForDisplayed({ timeout: 5000 });

    await driver.deleteSession();
}
executarTeste();
